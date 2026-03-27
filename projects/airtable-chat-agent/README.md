# Airtable Chat Support Agent

![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) ![Airtable](https://img.shields.io/badge/Airtable-F7D563?style=flat&logo=airtable&logoColor=black) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/airtable-chat-support-agent)**

AI-powered support agent that converts natural language questions into intelligent Airtable lookups. Query inventory levels, track sales history, process returns—all through conversational chat with barcode image recognition and multi-table awareness.

## What I Built

- **Natural Language → Airtable Queries** - GPT-4 understands business intent and automatically executes cross-table queries without manual navigation
- **Multi-Table Awareness** - Intelligently joins data across Inventory, Sales, and Returns tables to answer complex questions
- **Barcode Image Recognition** - Upload product photos or barcodes; system extracts codes and looks up associated data automatically
- **Session-Aware Conversations** - Maintains context across multiple questions so follow-ups reference previous results
- **Dual Frontend Options** - Deploy with Open WebUI for quick prototyping or custom React for branded experiences
- **Sub-Second Response Times** - Optimized queries return results in under 1 second for rapid support workflows
- **4 Comprehensive Screenshots** - Full workflow documentation with real-world query examples

## Architecture

```
User Chat Input
        ↓
  Open WebUI / Custom Frontend
        ↓
   n8n Workflow Engine
        ↓
  ┌─────┴──────┬──────────┬──────────┐
  ↓            ↓          ↓          ↓
Airtable    PostgreSQL   GPT-4    Vision API
(Tables)    (Sessions)  (Intent)  (Barcode)
```

**Process Flow:**
1. User asks question or uploads barcode image
2. GPT-4 analyzes intent and identifies required tables
3. n8n executes parallel Airtable queries across Inventory/Sales/Returns
4. Results normalized and formatted for context
5. GPT-4 generates natural language response
6. Session ID preserves context for follow-up questions
7. Multi-turn conversation maintains history

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Orchestration** | n8n | Workflow automation and multi-step processes |
| **AI Model** | OpenAI GPT-4 | Intent analysis, response generation |
| **Primary DB** | Airtable API | Inventory, Sales, Returns tables |
| **Session Storage** | PostgreSQL | Conversation context, audit logs |
| **Vision** | Barcode & Image Recognition | Product lookup from photos |
| **Frontend Options** | Open WebUI or React | User interface (pick one) |

## Key Features

### Multi-Table Awareness
Understands relationships between Inventory, Sales, and Returns tables. Queries automatically join data across multiple sources to answer complex questions like "what returns happened for this SKU in the last 30 days?" without manual table selection.

### Barcode Image Recognition
Users can upload product photos or barcode images. The system extracts the barcode and looks up associated inventory, pricing, and sales history automatically without typing.

### Session-Aware Conversations
Maintains conversation context so follow-up questions use previous results. "Show me returns for that product" understands which product was referenced earlier in the thread.

### Dual Frontend Options
Deploy with Open WebUI for rapid prototyping and testing, or build a custom React frontend for branded experiences. Both connect to the same n8n backend.

## Setup

Complete deployment instructions, Airtable base schema, n8n workflow exports, and API reference are available in the [full repository](https://github.com/702ron/airtable-chat-support-agent).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/airtable-chat-support-agent)*
