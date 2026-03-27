# n8n RAG AI Agent — Document Intelligence System

> A production-grade Retrieval-Augmented Generation (RAG) system built in n8n that lets users chat with their documents using natural language. Supports PDF, Excel, CSV, and Word files with automatic ingestion from Google Drive, vector search via PGVector, and intelligent re-ranking with Cohere.

---

## Problem

Businesses accumulate thousands of documents — spreadsheets, PDFs, reports, contracts — but finding specific information across them is painful. Traditional search is keyword-based and misses context. Employees waste hours digging through files instead of getting answers.

I needed a system that could: ingest documents automatically as they're added to a shared drive, understand the *content* of those documents (not just filenames), handle structured data (spreadsheets) differently from unstructured data (PDFs), and let anyone on the team ask plain-English questions and get accurate, sourced answers.

## Solution

A 54-node n8n workflow with three integrated subsystems:

1. **Conversational AI Agent** — An LLM-powered agent with four specialized tools (vector search, document listing, content retrieval, and tabular data queries) that can reason about which tool to use based on the question asked.

2. **Automated Document Ingestion Pipeline** — Google Drive triggers detect new or updated files, route them through format-specific extraction (PDF, Excel, CSV, Word), generate embeddings, and store them in PGVector for semantic search. Tabular data gets special treatment: rows are stored relationally *and* summarized for vector search.

3. **Garbage Collection System** — A scheduled process (every 15 minutes) checks the Google Drive trash, cross-references the database, and automatically purges deleted documents from the vector store and metadata tables.

## Architecture

```
                          ┌─────────────────────────────────────────────┐
                          │           QUERY LAYER                       │
                          │                                             │
    Chat UI ──────┐       │  ┌──────────┐    ┌─────────────────────┐   │
                  ├──────►│  │ Edit      │───►│   RAG AI Agent      │   │
    Webhook API ──┘       │  │ Fields    │    │   (OpenAI GPT-4)    │   │
                          │  └──────────┘    │                     │   │
                          │                  │  ┌─ List Documents   │   │
                          │                  │  ├─ Get File Content │   │
                          │                  │  ├─ Query Rows (SQL) │   │
                          │                  │  └─ Vector Search    │   │
                          │                  │     + Cohere Rerank  │   │
                          │                  └────────┬────────────┘   │
                          │                           │                 │
                          │              ┌────────────▼──────────┐     │
                          │              │   Postgres Chat Memory │     │
                          │              └───────────────────────┘     │
                          └─────────────────────────────────────────────┘

                          ┌─────────────────────────────────────────────┐
                          │        INGESTION LAYER                      │
                          │                                             │
  Google Drive ───────┐   │  ┌────────┐  ┌────────┐  ┌──────────────┐ │
   (File Created) ────┼──►│  │ Loop   │─►│Set File│─►│Delete Old    │ │
   (File Updated) ────┘   │  │ Items  │  │  ID    │  │Data + Docs   │ │
                          │  └────────┘  └────────┘  └──────┬───────┘ │
                          │                                  │         │
                          │              ┌───────────────────▼───────┐ │
                          │              │  Insert Document Metadata  │ │
                          │              └───────────────────┬───────┘ │
                          │                                  │         │
                          │              ┌───────────────────▼───────┐ │
                          │              │    Download from Drive     │ │
                          │              └───────────────────┬───────┘ │
                          │                                  │         │
                          │              ┌───────────────────▼───────┐ │
                          │              │   File Type Router         │ │
                          │              │   (Switch Node)            │ │
                          │              └──┬────┬────┬────┬────────┘ │
                          │                 │    │    │    │           │
                          │    ┌────────┐ ┌─┴──┐ │  ┌─┴──┐│           │
                          │    │ Excel  │ │CSV │ │  │Doc ││           │
                          │    │Extract │ │Ext │ │  │Ext ││           │
                          │    └───┬──┬─┘ └─┬──┘ │  └─┬──┘│           │
                          │        │  │     │    │    │   │           │
                          │        │  │     │    │    ▼   │           │
                          │    ┌───┘  └─────┘  ┌─┴──────┐ │           │
                          │    │               │PDF Ext │ │           │
                          │    ▼               └───┬────┘ │           │
                          │  ┌──────────────┐      │      │           │
                          │  │ Aggregate +  │      ▼      │           │
                          │  │ Summarize    │  ┌────────┐ │           │
                          │  │ (tabular)    │  │LangChn │ │           │
                          │  └──────┬───────┘  │ Code   │ │           │
                          │         │          └───┬────┘ │           │
                          │         ▼              │      │           │
                          │  ┌──────────────┐      │      │           │
                          │  │ Set Schema + │      │      │           │
                          │  │ Update Meta  │      │      │           │
                          │  └──────┬───────┘      │      │           │
                          │         │              │      │           │
                          │         ▼              ▼      │           │
                          │     ┌──────────────────────┐  │           │
                          │     │  PGVector Store       │  │           │
                          │     │  (OpenAI Embeddings + │  │           │
                          │     │   Text Splitter)      │  │           │
                          │     └──────────────────────┘  │           │
                          └─────────────────────────────────────────────┘

                          ┌─────────────────────────────────────────────┐
                          │       GARBAGE COLLECTION                    │
                          │                                             │
  Schedule ──────────────►│  Check Drive Trash ──► Parse Files          │
  (Every 15 min)          │       │                                     │
                          │       ▼                                     │
                          │  Exists in DB? ──► Delete Rows ──►         │
                          │                    Delete Docs ──►         │
                          │                    Delete Metadata          │
                          └─────────────────────────────────────────────┘
```

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Orchestration | **n8n** (self-hosted) | Workflow automation, triggers, routing |
| LLM | **OpenAI GPT-4** | Conversational AI, document summarization |
| Embeddings | **OpenAI Embeddings** | Text → vector conversion for semantic search |
| Re-ranking | **Cohere Rerank** | Improves retrieval accuracy by re-scoring results |
| Vector Store | **PostgreSQL + PGVector** | Stores and queries document embeddings |
| Memory | **Postgres Chat Memory** | Persists conversation history across sessions |
| File Storage | **Google Drive** | Source of truth for documents |
| Text Processing | **LangChain** (via n8n) | Document chunking, text splitting |
| API | **Webhook** | REST endpoint for external integrations |

## Key Features

### Multi-Format Document Intelligence
The system routes files through format-specific extraction pipelines. PDFs and Word docs get chunked via recursive character text splitting for semantic search. Excel and CSV files are treated differently — rows are stored in a relational table for precise SQL queries, while a summary is generated and embedded for natural language questions about the data.

### Dual Retrieval Strategy
The AI agent has access to **four tools** and decides which to use based on the question:
- **Vector Search** (PGVector + Cohere Reranker): For semantic questions like "What are the contract terms for vendor X?"
- **List Documents**: For discovery questions like "What documents do we have about shipping?"
- **Get File Contents**: For full-text retrieval of specific documents
- **Query Document Rows**: For precise tabular queries like "Show all invoices over $5,000"

### Automatic Lifecycle Management
Documents are automatically ingested when added to the Google Drive folder and automatically purged from the vector store when deleted. The 15-minute garbage collection cycle means the knowledge base stays current without any manual intervention. Updated files trigger a full re-ingestion (old embeddings deleted first, then re-processed).

### Production-Ready Patterns
- **Idempotent re-ingestion**: Old data is deleted before new data is inserted, preventing duplicates
- **Conversation memory**: Multi-turn conversations are persisted in Postgres, so context carries across questions
- **Dual entry points**: Both a chat UI and a webhook API, so the agent can be embedded in other applications
- **Schema tracking**: Tabular data schemas are stored in metadata, enabling the agent to understand column types and relationships

## Results

- Processes documents of any size with recursive text splitting (1,000-character chunks with 200-character overlap)
- Handles 5 file formats (PDF, XLSX, CSV, DOCX, TXT) through a single ingestion pipeline
- Sub-second query responses on typical document collections
- Zero-maintenance knowledge base — documents sync automatically from Google Drive
- Conversation context persists across sessions, eliminating repeated questions

## How to Deploy

### Prerequisites
- n8n instance (self-hosted or cloud)
- PostgreSQL with PGVector extension enabled
- OpenAI API key
- Cohere API key
- Google Drive API credentials

### Setup

1. **Database**: Create a PostgreSQL database with PGVector. The workflow automatically creates the required tables (`document_metadata` and `document_rows`) on first run.

2. **Import**: Import `workflow.json` into your n8n instance.

3. **Configure Credentials**:
   - OpenAI (API key)
   - Cohere (API key)
   - PostgreSQL (connection string)
   - Google Drive (OAuth2)

4. **Set Google Drive Folder**: Point the File Created and File Updated triggers at your target folder.

5. **Activate**: Enable the workflow. Drop files into the Google Drive folder and start chatting.

### Database Schema

```sql
-- Created automatically by the workflow
CREATE TABLE document_metadata (
    id SERIAL PRIMARY KEY,
    file_id TEXT UNIQUE,
    file_name TEXT,
    mime_type TEXT,
    schema_info JSONB,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE document_rows (
    id SERIAL PRIMARY KEY,
    file_id TEXT REFERENCES document_metadata(file_id),
    row_data JSONB,
    created_at TIMESTAMP DEFAULT NOW()
);

-- PGVector table (created by n8n's PGVector node)
-- Stores embeddings for semantic search
```

## Workflow Stats

| Metric | Value |
|--------|-------|
| Total Nodes | 54 |
| Connections | 42 |
| AI/LangChain Nodes | 10 |
| Database Operations | 12 |
| File Processing Nodes | 8 |
| Triggers | 4 (Chat, Webhook, 2x Drive, Schedule) |
| Sub-systems | 3 (Query, Ingestion, Garbage Collection) |

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — AI automation engineer specializing in n8n, Airtable, and LLM-powered business systems.*
