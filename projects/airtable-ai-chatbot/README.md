[![Chrome Extension](https://img.shields.io/badge/Chrome--Extension-MV3-orange)](https://developer.chrome.com/docs/extensions/mv3/)
[![AI Chatbot](https://img.shields.io/badge/AI-GPT--4-green)](https://openai.com/)
[![n8n](https://img.shields.io/badge/n8n-88--nodes-purple)](https://n8n.io/)
[![Airtable API](https://img.shields.io/badge/Airtable-data--source-blue)](https://airtable.com/api)

# Airtable AI Chatbot

I built an intelligent Chrome extension that injects an AI-powered chatbot directly into Airtable, enabling non-technical users to query data through natural language. Users ask questions like "What's in stock?" or "Who bought this product?" and receive instant answers by routing queries to the correct data lookup tools. The system combines GPT-4 semantic understanding with a 3-tool n8n backend architecture executing 88 workflow nodes total.

## What I Built

- **Chrome Extension** (Manifest V3): Dynamically injects AI chat widget into Airtable pages with Airtable-styled UI, keyboard shortcuts, and message history
- **inject.js** (3.2KB): Entry point loading n8n Chat SDK component on page load, handles DOM injection and event listeners
- **chat.bundle.es.js** (355KB): Compiled n8n Chat SDK providing the chat interface component with message rendering and input handling
- **AI Agent Workflow** (9 nodes): Core orchestration using OpenAI GPT-4 to understand intent and route queries to appropriate lookup tools
- **Webhook Entry Point** (11 nodes): Receives HTTP POST requests from browser extension, validates format, invokes main AI agent
- **Customer Lookup Tool** (25 nodes): Queries Airtable for customer records by email/name, returns account details with transaction history
- **Product/Lot Lookup Tool** (25 nodes): Finds inventory items by SKU or lot number, returns stock status across warehouses
- **Invoice Lookup Tool** (37 nodes): Retrieves transaction history and payment records, aggregates sales per customer

## Architecture

```
┌────────────────────────────────────────────────────────────┐
│        Airtable AI Chatbot Full-Stack Flow                │
├────────────────────────────────────────────────────────────┤
│                                                              │
│  Chrome Browser                                            │
│  ┌────────────────────────────────────────────────────┐   │
│  │           Airtable Base Page                       │   │
│  │                                                    │   │
│  │  inject.js (3.2KB)                               │   │
│  │  └─ Injects chat component on page load          │   │
│  │     └─ Loads chat.bundle.es.js (355KB)           │   │
│  │                                                    │   │
│  │  ┌──────────────────────────────────────┐        │   │
│  │  │  AI Chat Widget (600x800px)          │        │   │
│  │  │  - User input field                  │        │   │
│  │  │  - Message history with timestamps   │        │   │
│  │  │  - Airtable-styled buttons & colors │        │   │
│  │  │  - Keyboard: Esc=close, Ctrl+/=open │        │   │
│  │  │  - Loading spinner on pending query │        │   │
│  │  └──────────────────────────────────────┘        │   │
│  │         │ (Natural language query)               │   │
│  │         │ "What items are in stock?"             │   │
│  │         │ "Show me John's purchases"             │   │
│  │         ▼                                         │   │
│  │    n8n Webhook (HTTPS POST)                      │   │
│  └────────────────────────────────────────────────────┘   │
│         │                                                   │
│         ▼                                                   │
│  n8n Backend (Workflows)                                  │
│  ┌──────────────────────────────────────────────────┐    │
│  │  702 Airtable Agent Webhook (11 nodes)          │    │
│  │  └─ Receives HTTP POST from extension            │    │
│  │     - Parse JSON request body                    │    │
│  │     - Validate message format                    │    │
│  │     - Call main AI agent workflow                │    │
│  │                                                  │    │
│  │  702 Airtable Agent (9 nodes)                   │    │
│  │  ├─ OpenAI GPT-4 Call (semantic understanding)  │    │
│  │  ├─ System prompt: identify user intent         │    │
│  │  │  (customer lookup, inventory search, sales)  │    │
│  │  ├─ Determine required lookup tool              │    │
│  │  ├─ Call appropriate lookup tool                │    │
│  │  └─ Format response for chat display            │    │
│  │                                                  │    │
│  │  Lookup Tools (Executed in Parallel)            │    │
│  │  ├─ airtable_customer_lookup_tool (25 nodes)    │    │
│  │  │  └─ Query Inventory + Sales tables           │    │
│  │  ├─ airtable_lotNumber_lookup_tool (25 nodes)   │    │
│  │  │  └─ Find products by SKU/lot ID              │    │
│  │  └─ airtable_invoice_lookup (37 nodes)          │    │
│  │     └─ Retrieve transaction history              │    │
│  │                                                  │    │
│  │  Airtable API (Real-Time Data)                  │    │
│  │  ├─ Inventory table (SKU, qty, warehouse)       │    │
│  │  ├─ Sales table (customer, items, date)         │    │
│  │  └─ Returns table (refunds, adjustments)        │    │
│  └──────────────────────────────────────────────────┘    │
│         │                                                   │
│         ▼                                                   │
│  Response Stream (Server-Sent Events)                    │
│  └─ AI response flows back to chat widget                 │
│     - Chunked streaming for fast feedback                 │
│     - Error handling with user-friendly messages         │
│     - Related questions suggested                         │
│                                                             │
│  User sees: "Found 23 items in stock. Click to filter."  │
│                                                             │
└────────────────────────────────────────────────────────────┘
```

**Process Flow:**

1. **User Opens Airtable**: inject.js detects page load, dynamically loads n8n Chat SDK component into DOM
2. **Asks Question**: User types natural language query in chat widget (e.g., "What items are in stock?")
3. **Webhook Request**: Widget sends HTTP POST to n8n webhook with message content and conversation context
4. **Intent Recognition**: GPT-4 analyzes message, determines intent (customer lookup, inventory search, sales history)
5. **Tool Selection**: Main agent workflow selects appropriate lookup tool (customer/product/invoice) based on intent
6. **Parallel Lookup**: Lookup tool queries Airtable base with 25+ nodes handling filtering, aggregation, and formatting
7. **Response Assembly**: Main agent formats lookup results into conversational response with key details and next steps
8. **Stream to Widget**: Server-Sent Events stream response back to chat widget, which displays message with animations
9. **Conversation Memory**: Widget maintains message history, passes previous context to next query for multi-turn conversations

## Extension File Breakdown

| File | Size | Purpose |
|------|------|---------|
| **manifest.json** | 0.8KB | MV3 permissions (Airtable DOM access, n8n webhooks) |
| **inject.js** | 3.2KB | Page script that loads chat SDK and handles DOM injection |
| **chat.bundle.es.js** | 355KB | Compiled n8n Chat SDK component (React-based) |
| **popup.html** | 1.1KB | Extension icon popup UI (settings, enable/disable) |
| **styles.css** | 4.2KB | Chat widget styling to match Airtable design |
| **background.js** | 2.1KB | Service worker handling extension lifecycle |

## Backend Agent Tools

| Tool Name | Workflow Nodes | Data Source | What It Queries |
|-----------|----------|-------------|-----------------|
| **airtable_customer_lookup_tool** | 25 nodes | Airtable (Sales table) | Find customer by email/name, return orders, account history |
| **airtable_lotNumber_lookup_tool** | 25 nodes | Airtable (Inventory table) | Find product by SKU/lot ID, return qty, warehouse, cost |
| **airtable_invoice_lookup** | 37 nodes | Airtable (Transactions table) | Retrieve invoice by ID/date, return line items, payment status |
| **702 Airtable Agent** | 9 nodes | OpenAI + Tools | Main orchestration: understand intent, select tool, format response |
| **702 Airtable Agent Webhook** | 11 nodes | HTTP + Agent | Entry point: receive request, validate, invoke main agent |

**Total: 88 workflow nodes** across all tools providing reliability and comprehensive error handling.

## Example Chat Interaction

**User:** "What items are in stock?"

**Agent Process:**
1. GPT-4 recognizes this as an inventory query
2. Invokes airtable_lotNumber_lookup_tool
3. Tool queries Inventory table: `WHERE qty > 0`
4. Returns: 23 SKUs with quantities and warehouse locations

**Response:** "Found 23 items in stock across all warehouses. Top items: Blue Cotton Shirt (47 units, WP2), Black Leather Belt (12 units, WP3), White Polo (8 units, WP4). Would you like to filter by warehouse or price range?"

---

**User:** "Show me what John bought last month"

**Agent Process:**
1. GPT-4 recognizes customer lookup + time filter
2. Invokes airtable_customer_lookup_tool
3. Tool queries Sales table: `WHERE customer_name = 'John' AND date >= 30 days ago`
4. Returns: 5 transactions with items, dates, amounts

**Response:** "John made 5 purchases last month totaling $287.45: (1) Blue Cotton Shirt on 3/5, (2) Black Leather Belt on 3/12, (3) White Polo on 3/18, (4) Gray Sweater on 3/22, (5) Navy Jeans on 3/27. Would you like details on any of these orders?"

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Extension Framework** | Chrome Extension MV3 | Secure manifest, content scripts, background worker |
| **Chat Component** | n8n Chat SDK | Pre-built message interface with streaming support |
| **AI Engine** | OpenAI GPT-4 (gpt-4-turbo) | Natural language understanding and intent routing |
| **Backend Orchestration** | n8n (88 nodes total) | Workflow coordination and data retrieval |
| **Data Source** | Airtable API v0 | Real-time business data (Inventory, Sales, Returns) |
| **Communication** | Webhooks, HTTP POST, SSE | Browser ↔ n8n ↔ Airtable request/response |
| **Styling** | Custom CSS + Airtable design tokens | Chat widget matches Airtable UI appearance |

## Key Features

### Seamless Chrome Extension Integration
Manifest V3 compliance ensures modern security standards and future Chrome compatibility. inject.js dynamically loads on every Airtable page without configuration. n8n Chat SDK component provides a polished chat interface with message history and loading indicators. Custom CSS styling matches Airtable's design system so users feel like the chatbot is native. Keyboard shortcuts (Esc to close, Ctrl+/ to open) enable power users to work faster.

### AI-Powered Natural Language Queries
OpenAI GPT-4 provides semantic understanding of user intent, handling complex multi-step questions like "Show me high-value customers from last month." Intent recognition routes to correct lookup tool without user specifying which table to query. Multi-turn conversation support maintains context across messages, enabling follow-up questions. Clarification questions help disambiguate when user's intent is unclear.

### Multi-Table Lookup Architecture
Customer lookup tool handles account queries, purchase history, contact information with 25 specialized nodes. Product/lot lookup tool finds inventory by SKU or ID, returns stock levels across warehouses with pricing. Invoice lookup tool retrieves transaction details, payment status, and line items for financial audits. Parallel execution of multiple tools enables complex queries that combine customer + inventory + sales data.

### Production-Ready Workflows
702 Airtable Agent (9 nodes) provides core orchestration with GPT-4 integration and tool selection. 702 Airtable Agent Webhook (11 nodes) exposes HTTP entry point with request validation and error handling. 88+ total nodes across all lookup tools provide reliability—each tool has comprehensive error handling, retries, and detailed logging. Server-Sent Events streaming provides fast feedback to users while backend completes complex queries.

## Results & Impact

- **Democratized data access** for non-technical team members—no more "can you run that query?"
- **Reduced query time** from 5 minutes (find the spreadsheet, write formula) to 10 seconds (ask chatbot)
- **Increased data literacy** by making data exploration feel like natural conversation
- **Unified interface** for querying Inventory, Sales, and Returns tables without learning Airtable formula syntax
- **Seamless integration** with existing Airtable workflows—bot provides info without changing how people work
- **Scalable architecture** supporting 88 workflow nodes enables adding new data sources without code changes

## Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/702ron/airtable-ai-chatbot.git
   cd airtable-ai-chatbot
   ```

2. **Install extension dependencies**
   ```bash
   npm install
   ```

3. **Configure n8n API credentials**
   - Get n8n instance URL (self-hosted or cloud)
   - Get webhook URL from 702 Airtable Agent Webhook workflow
   - Add to extension config:
   ```bash
   export N8N_WEBHOOK_URL=https://your-n8n.com/webhook/airtable-agent
   ```

4. **Configure Airtable API**
   - Get personal access token from Airtable account settings
   - Get base ID from Airtable URL
   - Add to n8n credentials:
   ```
   AIRTABLE_API_KEY=your_token
   AIRTABLE_BASE_ID=your_base_id
   ```

5. **Configure OpenAI API**
   - Get API key from OpenAI dashboard
   - Add to n8n credentials:
   ```
   OPENAI_API_KEY=your_key
   ```

6. **Build and load extension**
   ```bash
   npm run build
   # Open Chrome and go to chrome://extensions/
   # Enable "Developer mode"
   # Click "Load unpacked" and select the dist/ folder
   ```

7. **Deploy n8n workflows**
   - Import workflows from `/workflows/` directory
   - Activate all workflows in n8n UI
   - Test webhook connectivity

## Security Notes

- Store API keys (OpenAI, Airtable, n8n) in secure n8n credential system, never in extension code
- Webhook URL should be HTTPS only—never send requests over HTTP
- Implement request signing to verify messages originated from trusted extension (HMAC-SHA256)
- Rate limit webhook to 100 requests/minute per IP to prevent abuse
- Airtable API token should have minimal scopes—read-only access to required tables only
- Sanitize GPT-4 responses before displaying to prevent prompt injection attacks
- Enable CORS validation on n8n webhook to only accept requests from extension
- Audit all Airtable queries in logs monthly for data access compliance
- Implement automatic logout after 24 hours of inactivity
- Never log conversation content that includes PII—sanitize before storing logs

## License

MIT

---

Built by [Ron](https://github.com/702ron)
