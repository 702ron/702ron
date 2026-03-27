# Airtable AI Chatbot

Chrome Extension for Natural Language Data Access — Embed AI-powered Airtable querying directly into your browser.

## Problem

Airtable contains critical business data, but querying across multiple tables (Inventory, Sales, Returns) requires switching contexts and writing formulas. Non-technical users struggle to answer questions like "What items are in stock?" or "Who bought this product?" Natural language interfaces lower the barrier to data access, but building one requires complex backend infrastructure.

## Solution

Built an end-to-end Chrome extension that injects an AI chatbot into any Airtable page:

**Frontend (Chrome Extension)**
- Manifest V3 compliant extension
- inject.js (3.2KB): Dynamically loads chatbot into Airtable DOM
- chat.bundle.es.js (355KB): Compiled n8n Chat SDK component
- Custom styled chat window (600x800px) matching Airtable UI
- Works seamlessly alongside Airtable native interface

**Backend (n8n Workflows)**
- **702 Airtable Agent** (9 nodes, ACTIVE): Core AI agent with natural language understanding
- **702 Airtable Agent Webhook** (11 nodes, ACTIVE): Webhook entry point for chat requests
- **airtable_customer_lookup_tool** (25 nodes): Customer record retrieval
- **airtable_lotNumber_lookup_tool** (25 nodes): Product lot and inventory lookup
- **airtable_invoice_lookup** (37 nodes): Invoice and transaction history

All workflows use OpenAI GPT-4 for semantic understanding and Airtable API for data retrieval.

```
┌────────────────────────────────────────────────────────────┐
│           Airtable AI Chatbot Full-Stack Flow              │
├────────────────────────────────────────────────────────────┤
│                                                              │
│  Chrome Browser                                            │
│  ┌───────────────────────────────────────────────────┐    │
│  │            Airtable Base Page                     │    │
│  │                                                   │    │
│  │  inject.js (3.2KB)                              │    │
│  │  └─ Injects chat component on page load         │    │
│  │                                                   │    │
│  │  ┌──────────────────────────────────────┐       │    │
│  │  │  AI Chat Widget (600x800px)          │       │    │
│  │  │  chat.bundle.es.js (355KB)           │       │    │
│  │  │  - User input field                  │       │    │
│  │  │  - Message history                   │       │    │
│  │  │  - Airtable-styled UI                │       │    │
│  │  │  - Keyboard shortcuts                │       │    │
│  │  └──────────────────────────────────────┘       │    │
│  │         │ (Natural language query)               │    │
│  │         │ "What items are in stock?"             │    │
│  │         ▼                                         │    │
│  │    n8n Webhook                                   │    │
│  └───────────────────────────────────────────────────┘    │
│         │                                                   │
│         ▼                                                   │
│  n8n Backend (Workflows)                                  │
│  ┌────────────────────────────────────────────────┐       │
│  │  702 Airtable Agent Webhook (11 nodes)        │       │
│  │  └─ Receives HTTP POST from extension          │       │
│  │     - Validates request format                 │       │
│  │     - Calls AI agent                           │       │
│  │                                                 │       │
│  │  702 Airtable Agent (9 nodes)                  │       │
│  │  ├─ OpenAI GPT-4 (semantic understanding)      │       │
│  │  ├─ Determine user intent                      │       │
│  │  ├─ Route to appropriate lookup tool           │       │
│  │  └─ Return natural language response           │       │
│  │                                                 │       │
│  │  Lookup Tools (Parallel Queries)               │       │
│  │  ├─ airtable_customer_lookup_tool (25 nodes)   │       │
│  │  ├─ airtable_lotNumber_lookup_tool (25 nodes)  │       │
│  │  └─ airtable_invoice_lookup (37 nodes)         │       │
│  │                                                 │       │
│  │  Airtable API                                  │       │
│  │  ├─ Inventory table queries                    │       │
│  │  ├─ Sales table aggregations                   │       │
│  │  └─ Returns table lookups                      │       │
│  └────────────────────────────────────────────────┘       │
│         │                                                   │
│         ▼                                                   │
│  Response Stream (Server-Sent Events)                     │
│  └─ AI response flows back to chat widget                 │
│                                                              │
│  User sees: "Found 23 items in stock. Click to filter."   │
│                                                              │
└────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Extension** | Chrome Extension (MV3), JavaScript | Browser injection & UI |
| **Chat Component** | n8n Chat SDK | Message interface |
| **AI Engine** | OpenAI GPT-4 | Natural language understanding |
| **Backend** | n8n workflows | Orchestration & data retrieval |
| **Database** | Airtable API | Business data source |
| **Communication** | Webhooks, HTTP, SSE | Real-time messaging |
| **Styling** | Custom CSS | Airtable UI integration |

## Key Features

### Seamless Chrome Extension Integration
- Manifest V3 compliant for modern Chrome security
- inject.js dynamically loads on Airtable pages
- n8n Chat SDK component provides polished chat interface
- Custom styling matches Airtable design system
- No user setup required beyond install

### AI-Powered Natural Language Queries
- OpenAI GPT-4 semantic understanding
- Intent recognition for routing to correct data source
- Multi-turn conversation support
- Clarification questions for ambiguous queries
- Contextual responses based on Airtable data

### Multi-Table Lookup Architecture
- Customer lookup for account-based queries
- Product/lot number lookup for inventory questions
- Invoice lookup for transaction history
- Parallel execution of multiple lookup tools
- Combined result presentation to user

### Production-Ready Workflows
- 702 Airtable Agent (9 nodes): Core orchestration
- 702 Airtable Agent Webhook (11 nodes): HTTP entry point
- 88+ total nodes across all lookup tools
- Comprehensive error handling
- Rate limiting and security validation

## Results & Impact

- **Democratized data access** for non-technical team members
- **Reduced query time** from "find the spreadsheet" to 10-second chat response
- **Increased data literacy** by making queries feel natural and conversational
- **Unified interface** for querying Inventory, Sales, and Returns tables
- **Seamless integration** with existing Airtable workflows
- **Scalable architecture** supporting 88+ workflow nodes for reliability

## License

MIT

---

Built by [Ron](https://github.com/702ron)
