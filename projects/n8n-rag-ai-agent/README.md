[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-PGVector-blue)](https://www.postgresql.org)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-brightgreen)](https://openai.com)
[![MIT License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

# n8n RAG AI Agent — Production Document Intelligence System

A production-grade Retrieval-Augmented Generation (RAG) system that transforms document collections into a conversational knowledge base. Automatically ingest PDFs, Excel, CSV, and Word files from Google Drive, embed them into a vector database, and let users ask natural language questions with AI-powered retrieval and re-ranking for accurate, sourced answers.

## What I Built

**54-node n8n workflow system** with three integrated subsystems handling document ingestion, intelligent query processing, and garbage collection:

- **Conversational AI Agent** — LLM-powered reasoning engine with four specialized tools (vector search, document listing, content retrieval, SQL queries) that dynamically selects the best strategy based on user questions
- **Automated Document Ingestion Pipeline** — Google Drive triggers detect new/updated files, route through format-specific extractors (PDF, Excel, CSV, Word), generate OpenAI embeddings, and persist in PGVector for semantic search
- **Dual Retrieval Strategy** — Structured data (spreadsheets) stored relationally *and* summarized for vectors; unstructured data chunked via recursive character splitting for context preservation
- **Garbage Collection System** — Scheduled process (every 15 min) monitors Google Drive trash, cross-references database, automatically purges deleted documents from vector store and metadata
- **Conversation Memory** — Persisted in PostgreSQL so multi-turn interactions maintain context across sessions without data loss

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

**Process Flow:**

1. **File Detection** — Google Drive trigger detects new or updated files; workflow extracts file metadata (ID, name, MIME type)
2. **Metadata Registration** — Document metadata inserted into PostgreSQL table with timestamps for tracking and deduplication
3. **Format-Aware Extraction** — Router node branches to format-specific handlers: Excel/CSV rows extracted to JSONB, PDFs/Word chunked via LangChain text splitter (1000-char chunks, 200-char overlap)
4. **Dual Storage Strategy** — Tabular data stored in relational `document_rows` table *and* summarized for embedding; unstructured text chunked and embedded directly
5. **Vector Embedding & Indexing** — OpenAI Embeddings API converts text to 1536-dimensional vectors; Cohere Rerank re-scores results for improved retrieval accuracy
6. **Query Routing** — When user asks a question, AI agent analyzes intent and selects optimal tool: vector search for semantic queries, SQL for precise data lookups, document listing for discovery
7. **Garbage Collection Cycle** — Every 15 minutes, scheduled job checks Google Drive trash against database; deletes orphaned embeddings, rows, and metadata to keep knowledge base current

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Orchestration** | n8n (self-hosted or cloud) | Workflow automation, triggers, routing, API calls |
| **LLM & Reasoning** | OpenAI GPT-4 | Conversational AI, multi-tool agent, response generation |
| **Embeddings** | OpenAI Embeddings (text-embedding-3-small) | Text-to-vector conversion for semantic search |
| **Re-ranking** | Cohere Rerank API | Improves retrieval accuracy by re-scoring BM25 results |
| **Vector Database** | PostgreSQL with pgvector extension | Stores and queries document embeddings with HNSW indexing |
| **Chat Memory** | PostgreSQL (native tables) | Persists conversation history across sessions |
| **Document Storage** | Google Drive | Source of truth for all documents; backup and audit trail |
| **Text Processing** | LangChain (via n8n LangChain node) | Recursive character text splitting, context preservation |
| **API Gateway** | n8n Webhook | REST endpoint for external integrations and chat UI |

## Key Features

### Multi-Format Document Intelligence
The system routes files through format-specific extraction pipelines. PDFs and Word documents are chunked via recursive character text splitting (1,000-character chunks with 200-character overlap) for optimal semantic search. Excel and CSV files receive special treatment: rows are stored in the relational `document_rows` table for precise SQL queries, while a concise summary is generated and embedded for natural language questions about the data.

### Dual Retrieval Strategy
The AI agent has access to **four independent tools** and dynamically selects the best one based on question intent:
- **Vector Search** (PGVector + Cohere Reranker): For semantic questions like "What are the contract renewal terms for vendor X?"
- **Query Document Rows**: For precise tabular queries like "Show all invoices over $5,000 from last quarter"
- **List Documents**: For discovery-focused questions like "What documents do we have about shipping policies?"
- **Get File Contents**: For full-text retrieval when users need the complete document

### Automatic Lifecycle Management
Documents are automatically ingested when added to the Google Drive folder and automatically purged when deleted. The 15-minute garbage collection cycle ensures the knowledge base stays current without manual cleanup. Updated files trigger idempotent re-ingestion: old embeddings are deleted first, then new data is processed and inserted, preventing duplicates.

### Production-Ready Patterns
- **Idempotent re-ingestion**: Old data deleted before new data inserted, preventing duplicates and corruption
- **Conversation memory**: Multi-turn conversations persisted in Postgres preserve context across sessions and browser reloads
- **Dual entry points**: Both chat UI and webhook API allow embedding the agent into Slack, custom frontends, or third-party apps
- **Schema tracking**: Tabular data schemas stored in metadata, enabling the agent to understand column types, relationships, and data constraints

## Database Schema

```sql
-- Created automatically by the workflow on first run
CREATE TABLE document_metadata (
    id SERIAL PRIMARY KEY,
    file_id TEXT UNIQUE NOT NULL,
    file_name TEXT NOT NULL,
    mime_type TEXT,
    schema_info JSONB,  -- For tabular data: column names, types, row count
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE document_rows (
    id SERIAL PRIMARY KEY,
    file_id TEXT NOT NULL REFERENCES document_metadata(file_id) ON DELETE CASCADE,
    row_index INTEGER,  -- Original row number from source file
    row_data JSONB NOT NULL,  -- {column1: value1, column2: value2, ...}
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_document_rows_file_id ON document_rows(file_id);
CREATE INDEX idx_document_metadata_file_id ON document_metadata(file_id);

-- pgvector table (auto-created by n8n PGVector node)
CREATE TABLE documents_embeddings (
    id BIGSERIAL PRIMARY KEY,
    content TEXT,
    embedding vector(1536),
    metadata JSONB,  -- {file_id, chunk_index, chunk_type}
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_documents_embeddings_metadata ON documents_embeddings USING GIN (metadata);
CREATE INDEX idx_documents_embeddings_vector ON documents_embeddings USING HNSW (embedding vector_cosine_ops);
```

## Workflow Stats

| Metric | Value |
|--------|-------|
| **Total Nodes** | 54 |
| **Connections** | 42 |
| **AI/LLM Nodes** | 10 (OpenAI, Cohere, LangChain) |
| **Database Operations** | 12 (INSERT, SELECT, DELETE on metadata/rows/embeddings) |
| **File Processing Nodes** | 8 (Excel, CSV, PDF, Word extractors) |
| **Active Triggers** | 4 (Chat UI, Webhook, 2× Google Drive, Scheduled GC) |
| **Sub-systems** | 3 (Query Agent, Document Ingestion, Garbage Collection) |
| **Supported File Formats** | 5 (PDF, XLSX, CSV, DOCX, TXT) |

## Setup

### Prerequisites
- n8n instance (self-hosted on Docker/Linux or n8n Cloud)
- PostgreSQL database with pgvector extension (`CREATE EXTENSION IF NOT EXISTS vector;`)
- OpenAI API key (for GPT-4 and embeddings)
- Cohere API key (for re-ranking)
- Google Drive API credentials (OAuth2)

### Step-by-Step Installation

1. **Create PostgreSQL Database**
   ```bash
   # Connect to your PostgreSQL instance
   psql -U postgres

   # Create database
   CREATE DATABASE rag_documents;

   # Enable pgvector extension
   \c rag_documents
   CREATE EXTENSION IF NOT EXISTS vector;

   # Verify installation
   SELECT * FROM pg_extension;
   ```

2. **Import Workflow into n8n**
   - Log into your n8n instance
   - Navigate to Workflows → Import
   - Upload the exported `rag_workflow.json` from this repository
   - The workflow will auto-create required tables on first run

3. **Configure Credentials in n8n**
   - **OpenAI**: Settings → Credentials → Add OpenAI credential (API key)
   - **Cohere**: Settings → Credentials → Add HTTP Basic Auth credential (API key as password)
   - **PostgreSQL**: Settings → Credentials → Add PostgreSQL connection (host, port, database, user, password)
   - **Google Drive**: Settings → Credentials → Add Google OAuth2 (authorize access to target folder)

4. **Configure Workflow Parameters**
   - Open the imported workflow
   - In the **Google Drive File Created** trigger node, select your target Google Drive folder
   - In the **Google Drive File Updated** trigger node, select the same folder
   - Set `CHUNK_SIZE` to 1000 and `CHUNK_OVERLAP` to 200 in the LangChain text splitter node
   - Verify all credential references are properly linked

5. **Test End-to-End**
   - Upload a small PDF or CSV to your target Google Drive folder
   - Monitor the workflow execution in n8n (should complete in 10–30 seconds depending on file size)
   - Check PostgreSQL: `SELECT COUNT(*) FROM document_metadata;` should show 1 row
   - Query the chat UI or webhook API with: `{"question": "What files did you ingest?"}`
   - Expected response: Lists the test file with metadata

6. **Activate for Production**
   - Enable all triggers in the workflow editor
   - Schedule the Garbage Collection subprocess to run every 15 minutes
   - Set up error handling webhooks or Slack notifications for failed ingestions
   - Monitor database disk usage and implement retention policies if needed

### Example Webhook Request

```bash
# Ask a semantic question
curl -X POST http://localhost:3000/webhook/your-webhook-id \
  -H "Content-Type: application/json" \
  -d '{
    "question": "What are the key terms and conditions in our vendor contracts?",
    "conversation_id": "user-123",
    "top_k": 5
  }'

# Response example:
{
  "answer": "Based on the vendor contracts in your knowledge base, the key terms are: 1) Payment terms of Net 30, 2) Minimum order quantities vary by product category, 3) Quarterly price adjustments tied to commodity indices, 4) 90-day termination notice period for both parties...",
  "sources": [
    {
      "file_name": "Vendor_Agreement_2024.pdf",
      "chunk": "Payment terms net 30 days from invoice...",
      "relevance_score": 0.94
    }
  ]
}
```

## Security Notes

- **API Keys**: Store OpenAI, Cohere, and Google credentials in n8n's encrypted credential vault, never in workflow code
- **Google Drive Access**: Use OAuth2 with minimal scopes (read-only on target folder, no account-wide access)
- **Database Authentication**: Use strong PostgreSQL passwords; consider IP whitelisting if self-hosted
- **Vector Data Privacy**: Embeddings stored in PostgreSQL; no third-party access to raw document content
- **Conversation Memory**: Chat history persisted in PostgreSQL; implement row-level security if handling PII
- **File Handling**: Temporary files downloaded from Google Drive stored in n8n's encrypted temp directories, deleted after processing
- **Rate Limiting**: Implement request throttling on the webhook API to prevent abuse (recommend 10 req/min per user)

## License

MIT

---

Built by [Ron](https://github.com/702ron) — AI automation engineer specializing in n8n, RAG systems, and LLM-powered business applications.
