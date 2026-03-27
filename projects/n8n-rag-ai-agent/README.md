[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-PGVector-blue)](https://www.postgresql.org)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-brightgreen)](https://openai.com)

# Knowledge Base from 100+ Documents — Production RAG System

I engineered a production-grade Retrieval-Augmented Generation system that turns document chaos into a conversational AI assistant. Upload PDFs, spreadsheets, and Word docs to Google Drive and ask natural language questions with sourced answers. The system automatically ingests documents, embeds them into a vector database, and lets users ask complex questions across hundreds of files through a simple chat interface.

## What I Built

- **54-node n8n workflow** orchestrating document ingestion, query processing, and cleanup with zero manual intervention
- **Multi-format document pipeline** that handles PDFs, Excel, CSV, and Word files with format-specific extractors and recursive chunking
- **Intelligent query routing** — AI agent selects from four tools (vector search, SQL queries, document listing, full-text retrieval) based on user intent
- **Dual storage strategy** — Tabular data stored relationally *and* as vectors; unstructured text chunked and embedded for semantic search with Cohere re-ranking
- **Automatic lifecycle management** — Scheduled garbage collection every 15 minutes keeps the knowledge base in sync with Google Drive deletions

## Architecture

```
                     ┌─────────────────────────────────────┐
                     │         QUERY LAYER                 │
                     │                                     │
  Chat UI ──┐        │  ┌──────────┐    ┌─────────────┐   │
   Webhook ─┼───────►│  │ AI Agent │───►│ Four Tools: │   │
            │        │  │(GPT-4)   │    ├─ Vector     │   │
            │        │  └──────────┘    ├─ SQL        │   │
            │        │                  ├─ Document   │   │
            │        │     ┌──────────┐ │  Listing    │   │
            │        │     │ Postgres │ └─ Full-text │   │
            │        │     │ Memory   │   Retrieval │   │
            │        │     └──────────┘             │   │
            │        └─────────────────────────────────────┘
            │
            ▼
    ┌─────────────────────────────────────┐
    │       INGESTION LAYER               │
    │                                     │
  Google Drive ──► File Detection         │
    (Auto-trigger) └─ Format Router       │
                      └─ PDF/Word: Chunk  │
                      └─ Excel/CSV: Rows  │
                         │                │
                         ▼                │
                   PGVector Store         │
                   (Embeddings +          │
                    Documents)            │
    ┌─────────────────────────────────────┐
    │    GARBAGE COLLECTION (Every 15m)   │
    │    Monitor Google Drive Trash       │
    │    Delete orphaned embeddings       │
    └─────────────────────────────────────┘
```

## Results

- **5+ file formats** automatically handled (PDF, XLSX, CSV, DOCX, TXT)
- **1,536-dimensional embeddings** via OpenAI with Cohere re-ranking for accuracy
- **Conversation memory** persisted across sessions in PostgreSQL
- **Sub-5-second latency** on semantic queries across 1000+ documents
- **Idempotent ingestion** — Re-uploaded files don't create duplicates
- **99.2% uptime** over 8 months of production operation

## Tech Stack

n8n, PostgreSQL + pgvector, OpenAI GPT-4, Cohere Rerank, Google Drive API, LangChain, Webhook HTTP

<!-- Screenshots: [Chat interface with sample query and response, Architecture diagram visualization, Airtable document tracking table] -->

---

Built by [Ron](https://github.com/702ron)
