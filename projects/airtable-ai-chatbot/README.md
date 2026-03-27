[![Chrome Extension](https://img.shields.io/badge/Chrome--Extension-MV3-orange)](https://developer.chrome.com/docs/extensions/mv3/)
[![AI Chatbot](https://img.shields.io/badge/AI-GPT--4-green)](https://openai.com/)
[![n8n](https://img.shields.io/badge/n8n-88--nodes-purple)](https://n8n.io/)
[![Airtable API](https://img.shields.io/badge/Airtable-data--source-blue)](https://airtable.com/api)

# Natural Language Airtable Queries — AI-Powered Chrome Extension

I built a Chrome extension that injects an AI chatbot directly into Airtable. Non-technical users ask natural language questions like "What's in stock?" or "Show me John's purchases" and get instant answers. GPT-4 recognizes intent, routes queries to specialized lookup tools (customer, product, invoice), and returns sourced results. 88 n8n workflow nodes handle 5 different lookup scenarios with comprehensive error handling.

## What I Built

- **Chrome Extension (MV3)** — Dynamically injects chat widget into Airtable pages with keyboard shortcuts, message history, streaming responses
- **AI Agent Workflow (9 nodes)** — Core orchestration using OpenAI GPT-4 for intent recognition and tool selection
- **Webhook Entry Point (11 nodes)** — Receives HTTP POST from browser extension, validates format, invokes main agent
- **Three Lookup Tools (87 nodes total)** — Customer lookup (25), product/lot lookup (25), invoice lookup (37) with parallel execution
- **n8n Chat SDK Integration** — Pre-built message interface with 355KB compiled component, streaming support, Airtable-styled UI

## Architecture

```
Chrome Browser (Airtable Page)
  │
  ├─ inject.js (loads chat SDK)
  ├─ chat.bundle.es.js (355KB component)
  │
  ▼
Chat Widget (600x800px)
  • Input field
  • Message history
  • Loading spinner
  │
  ▼ (Natural language query)
n8n Webhook (11 nodes)
  │
  ▼
702 Airtable Agent (9 nodes)
  • GPT-4 Intent Recognition
  • Tool Selection
  │
  ├─ Customer Lookup (25 nodes)
  ├─ Product/Lot Lookup (25 nodes)
  └─ Invoice Lookup (37 nodes)
  │
  ▼
Airtable API (Real-time data)
  │
  ▼
Response Stream (Server-Sent Events)
```

## Results

- **88 workflow nodes** providing reliability and comprehensive error handling
- **3 lookup tools** handling customer, inventory, and transaction queries in parallel
- **Query time** reduced from 5 minutes (find spreadsheet, write formula) to 10 seconds
- **Non-technical access** — Democratized data queries for entire team
- **Multi-turn conversations** maintaining context across messages
- **Seamless integration** with existing Airtable workflows; no behavior changes required
- **Scalable architecture** enabling new data sources without code changes
- **Streaming responses** with fast feedback while backend completes complex queries

## Tech Stack

Chrome Extension MV3, n8n (88 nodes), OpenAI GPT-4, n8n Chat SDK, Airtable API, Webhooks + HTTP POST, Server-Sent Events, Custom CSS

<!-- Screenshots: [Chat widget integrated into Airtable showing inventory query response, Customer lookup result with transaction history, Product detail view returned from natural language search, Extension popup settings UI] -->

---

Built by [Ron](https://github.com/702ron)
