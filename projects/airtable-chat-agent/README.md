![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) ![Airtable](https://img.shields.io/badge/Airtable-F7D563?style=flat&logo=airtable&logoColor=black) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)

# Natural Language Interface for Business Data — AI Chat Agent

**[Full Repository](https://github.com/702ron/airtable-chat-support-agent)**

AI-powered support agent that converts plain English questions into intelligent Airtable lookups. Query inventory levels, track sales history, process returns — all through conversational chat with barcode image recognition and multi-table awareness.

![n8n Workflow](./screenshots/n8n_workflow.png)

## What I Built

- **Natural Language → Airtable Queries** — GPT-4 understands business intent and executes cross-table queries without manual navigation
- **Multi-Table Awareness** — Joins data across Inventory, Sales, and Returns to answer complex questions automatically
- **Barcode Image Recognition** — Upload product photos or barcodes; system extracts codes and looks up associated data
- **Session-Aware Conversations** — Maintains context across questions so follow-ups reference previous results
- **Dual Frontend** — Deploy with Open WebUI for quick prototyping or custom React for branded experiences

## Screenshots

| Chat Interface | Execution View |
|:-:|:-:|
| [![Chat UI](./screenshots/chat_ui.png)](./screenshots/chat_ui.png) | [![Execution](./screenshots/execution_view.png)](./screenshots/execution_view.png) |

| Airtable Data | Query Results |
|:-:|:-:|
| [![Airtable](./screenshots/airtable_inventory.png)](./screenshots/airtable_inventory.png) | [![Results](./screenshots/result_output.png)](./screenshots/result_output.png) |

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

## Results

- **Sub-second response times** on inventory and sales lookups
- **3 Airtable tables** queried simultaneously per request
- **Barcode recognition** from uploaded images — no typing required
- **Session memory** persisted in PostgreSQL across browser reloads

## Tech Stack

n8n, OpenAI GPT-4, Airtable API, PostgreSQL, Open WebUI, Barcode Recognition

---

Built by [Ron](https://github.com/702ron)
