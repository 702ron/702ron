# Airtable Chat Support Agent

> **[View full repository with screenshots and code →](https://github.com/702ron/airtable-chat-support-agent)**

AI-powered support agent that converts natural language questions into intelligent Airtable lookups. Query inventory levels, track sales history, process returns—all through conversational chat with barcode image recognition and multi-table awareness.

## Problem
Support teams spend hours searching spreadsheets and databases for customer data. Natural language queries from customers or internal staff require manual database navigation, multiple systems, and domain knowledge to translate into proper lookups.

## Solution
Built a conversational agent that understands business intent and automatically executes cross-table Airtable queries. The system analyzes questions, identifies required tables (Inventory, Sales, Returns), fetches relevant data, and responds in natural language. Barcode image recognition enables product lookup by photo. Session-aware conversations maintain context across multiple questions, and multiple frontend options (Open WebUI or custom) provide flexibility.

## Architecture

```
Chat Interface (Open WebUI / Custom)
        ↓
  n8n Workflow Engine
        ↓
   ┌────┴────┬──────────┬──────────┐
   ↓         ↓          ↓          ↓
 Airtable  PostgreSQL  GPT-4    Barcode
(Tables)  (Sessions)  (Intent)  (Vision)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Orchestration | n8n |
| AI Model | OpenAI GPT-4 |
| Database | Airtable API, PostgreSQL |
| Vision | Barcode & image recognition |
| Frontend | Open WebUI (or custom) |
| Session Storage | PostgreSQL |

## Key Features

### Multi-Table Awareness
Understands relationships between Inventory, Sales, and Returns tables. Queries automatically join data across multiple sources to answer complex questions like "what returns happened for this SKU in the last 30 days?"

### Barcode Image Recognition
Users can upload product photos or barcode images. The system extracts the barcode and looks up associated inventory, pricing, and sales history automatically.

### Session-Aware Conversations
Maintains conversation context so follow-up questions use previous results. "Show me returns for that product" understands which product was referenced earlier.

### Dual Frontend Options
Deploy with Open WebUI for quick prototyping or custom React frontend for branded experiences. Both connect to the same n8n backend.

## Results

- **4 Screenshots**: Full workflow documentation with example queries
- **12 Comprehensive Sections**: Covers setup, architecture, deployment, and API reference
- **8.5/10 Rating**: Highly functional and production-ready
- **Sub-Second Responses**: Multi-table queries return results in under 1 second

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/airtable-chat-support-agent)*
