[![n8n Workflows](https://img.shields.io/badge/n8n_Workflows-228+-orange?style=flat&logo=n8n&logoColor=white)](https://n8n.io)
[![Airtable Bases](https://img.shields.io/badge/Airtable_Bases-230+-blue?style=flat&logo=airtable&logoColor=white)](https://airtable.com)
[![Custom Scripts](https://img.shields.io/badge/Custom_Scripts-165+-brightgreen?style=flat)](.)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6?style=flat&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-412991?style=flat&logo=openai&logoColor=white)](https://openai.com)

# Ron — AI & Automation Engineer

I design and build production automation systems at the intersection of AI, data, and business operations. My work spans the full stack: LLM-powered agents that reason about business data, n8n workflows that orchestrate complex multi-step processes, web scrapers that feed pricing intelligence, and Airtable ecosystems that run entire businesses.

Everything listed here runs (or has run) in production — not demos, not tutorials, not toy projects.

```
 228+ n8n workflows built    ·    79 running in production daily
 230+ Airtable bases          ·    50+ active across 2 locations
 165+ automation scripts      ·    4+ years of continuous iteration
```

---

## Featured Projects

<table>
<tr>
<td width="50%">

### [AI Label Designer](./projects/ai-label-designer)
**[Live Demo](https://labelwizard.702market.com/)** · **[GitHub](https://github.com/702ron/1932-label-wizard)**

Full-stack AI image generation app — 4-step wizard that creates custom whiskey labels with AI-generated logos, backgrounds, and photorealistic bottle mockups.

`React` `FastAPI` `TypeScript` `Google Gemini` `OpenRouter` `Redis` `PostgreSQL` `MinIO`

</td>
<td width="50%">

### [Product Info Lookup API](./projects/product-info-lookup)
**[GitHub](https://github.com/702ron/product-info-lookup)**

Universal product data retrieval across Amazon, Walmart, Target, and Home Depot. Auto-detects identifiers, queries 6 APIs, AI-powered categorization.

`n8n` `NocoDB` `Google Gemini` `GPT-4` `Firecrawl` `Airtable`

</td>
</tr>
<tr>
<td width="50%">

### [Airtable Chat Support Agent](./projects/airtable-chat-agent)
**[GitHub](https://github.com/702ron/airtable-chat-support-agent)**

AI-powered natural language interface for business data. Converts English queries into structured lookups across Inventory, Sales, and Returns. Barcode image recognition.

`n8n` `GPT-4` `Airtable` `PostgreSQL` `Open WebUI`

</td>
<td width="50%">

### [Refund Returns Processing](./projects/refund-returns-system)
**[GitHub](https://github.com/702ron/refund-returns-processing)**

End-to-end returns automation with 7-step processing, 6 return types, multi-location support. RabbitMQ queuing ensures zero lost transactions.

`n8n` `RabbitMQ` `Stripe API` `Airtable` `Browserless`

</td>
</tr>
<tr>
<td colspan="2" align="center">

### [n8n Plain.com Node](./projects/n8n-plain-node)
**[GitHub](https://github.com/702ron/n8n-plain-node)** · **[npm](https://www.npmjs.com/package/n8n-nodes-plain)**

Open-source n8n community node for Plain.com customer support — GraphQL integration, 6 resources, real-time event triggers. Published to npm.

`TypeScript` `n8n` `GraphQL`

</td>
</tr>
</table>

---

## All Projects

### AI & Intelligent Agents

| Project | What It Does | Stack |
|---------|-------------|-------|
| **[RAG AI Agent](./projects/n8n-rag-ai-agent)** | 54-node n8n system with 4 specialized tools, automated document ingestion from Google Drive, PGVector semantic search, and Cohere re-ranking. Handles PDF, Excel, CSV, and Word. | n8n · GPT-4 · PGVector · Cohere |
| **[AI Label Designer](./projects/ai-label-designer)** &middot; [Live Demo](https://labelwizard.702market.com/) &middot; [Repo](https://github.com/702ron/1932-label-wizard) | Full-stack whiskey label creator with 4-step wizard, AI logo and background generation, photorealistic bottle mockup. React + FastAPI. | React · FastAPI · Gemini · Redis |
| **[Airtable Chat Agent](./projects/airtable-chat-agent)** &middot; [Repo](https://github.com/702ron/airtable-chat-support-agent) | Natural language interface for business data. Converts English queries into Airtable lookups across Inventory, Sales, and Returns. Barcode image recognition. | n8n · GPT-4 · Airtable · PostgreSQL |
| **[Airtable AI Chatbot](./projects/airtable-ai-chatbot)** | Chrome Manifest V3 extension injecting AI chat into Airtable. 355KB compiled n8n Chat SDK, 88+ workflow nodes, 5 specialized tools. | Chrome Extension · n8n · GPT-4 |
| **[AI Email Labeler](./projects/ai-email-labeler)** | 18-node classifier + 22-node Gmail Agent. Auto-labels incoming email with GPT-4, reads threads, summarizes, and drafts responses. Production daily. | n8n · GPT-4 · Gmail API |
| **[Resume Parser](./projects/resume-parser)** &middot; [Repo](https://github.com/702ron/resume-parser-airtable) | Automated recruitment: monitors Gmail, extracts 8 resume fields with GPT-4, stores in Drive, tracks in Airtable. | n8n · GPT-4 · Google Drive |
| **[Nostradamus AI](./projects/nostradamus-ai)** | 83 Python modules + 35 TypeScript components. Custom archaic French NLP, Neo4j knowledge graphs, ML pattern recognition, 11 scrapers, WebSocket streaming. | FastAPI · React · Neo4j · spaCy |
| **[Job Scraper + AI Scoring](./projects/job-scraper-ai-scoring)** | Flask app scraping 8+ job boards with AI scoring module that ranks descriptions against customizable criteria. 2MB+ SQLite history. | Python · Flask · OpenAI · SQLite |

---

## Business Automation & Operations

| Project | What It Does | Stack |
|---------|-------------|-------|
| **[HiBid Auction Automation](./projects/hibid-auction-automation)** | Thousands of monthly auctions. 42-node Lister, 25-node Watcher, Selenium/Playwright bid placement, Stripe + RabbitMQ payment processing. | n8n · Selenium · Stripe · RabbitMQ |
| **[Airtable Operations Platform](./projects/airtable-operations-platform)** | 230+ bases, 50+ active daily, 2 physical locations. Inventory, finance, sales, returns, HR, marketplace integrations. 426+ Airtable node uses across n8n. | Airtable · n8n · Supabase · Stripe |
| **[Daily Business Intelligence](./projects/daily-business-intelligence)** | 6 interconnected workflows (up to 62 nodes). Pulls HiBid sales, calculates KPIs, cross-references inventory/returns, delivers HTML reports at 9AM. React dashboard. | n8n · Airtable · React · Vite |
| **[Stripe Payment Automation](./projects/stripe-payment-automation)** | Airtable → RabbitMQ → n8n → Browserless void → Stripe refund → Airtable log. 21-node workflow + Python GUI + JS scripts. Zero lost transactions. | n8n · Stripe · RabbitMQ · Browserless |
| **[Refund Returns System](./projects/refund-returns-system)** &middot; [Repo](https://github.com/702ron/refund-returns-processing) | 7-step processing, 6 return types, multi-location. RabbitMQ queuing, browserless voids, Stripe refunds. Idempotent with audit logging. | n8n · RabbitMQ · Stripe · Airtable |
| **[Auction Management Webapp](./projects/auction-management-webapp)** | Django 5.0, 5 management scripts (37K+ lines each), Selenium uploads, void/refund processing, Airtable sync. Dockerized. 1,000+ auctions/month. | Django · PostgreSQL · Docker · Selenium |
| **[n8n Error Monitoring](./projects/n8n-error-monitoring)** | Centralized handler for 228+ workflows. Error → Airtable log → daily retry → self-healing → escalation. 85%+ auto-recovery rate. | n8n · Airtable · Gmail |

---

## Web Scraping & Data Pipelines

| Project | What It Does | Stack |
|---------|-------------|-------|
| **[Retail Product Scraper](./projects/retail-product-scraper)** | Modular suite: Macy's (Selenium), Lowe's (API + barcode + Amazon/CamelCamelCamel), Kohl's (4 versions), Amazon (ASIN/UPC/FNSKU), Google Trends. Feeds Airtable pricing. | Python · Selenium · Playwright · n8n |
| **[Product Info Lookup](./projects/product-info-lookup)** &middot; [Repo](https://github.com/702ron/product-info-lookup) | Universal lookup across Amazon, Walmart, Target, Home Depot. Auto-detects ID types, queries 6 APIs, NocoDB cache, AI categorization via Gemini + GPT-4. | n8n · NocoDB · Gemini · GPT-4 |
| **[CSV & Data Pipeline Tools](./projects/csv-data-pipeline-tools)** | ETL toolkit: Macy's manifest converter, pallet grouping for 81KB+ inventory files, HiBid image formatters, ZPL barcode label generators, auction exporters. | Python · pandas · Google Sheets API |
| **[Browser Automation Toolkit](./projects/browser-automation-toolkit)** | 4 frameworks in production: Selenium (250+ images/auction), Playwright on Windmill, Puppeteer for scraping, Browserless.io for cloud execution. Self-hosted Docker. | Selenium · Playwright · Puppeteer · Docker |

---

## Marketing & E-Commerce

| Project | What It Does | Stack |
|---------|-------------|-------|
| **[Marketplace Listing Automation](./projects/marketplace-listing-automation)** | Automated publishing to HiBid, OfferUp, eBay, Amazon, Liquidation.com. 42-node orchestrator, 250+ image uploads per auction, manifest-to-listing formatters. | n8n · Selenium · Playwright · Airtable |
| **[Mailchimp Automation Suite](./projects/n8n-mailchimp-automation-suite)** | 5 interconnected workflows: buyer sync, behavioral segmentation, MJML campaign generation, Mailchimp delivery, weekly list cleanup. | n8n · Mailchimp · MJML · Airtable |
| **[Email Campaign Generator](./projects/email-campaign-generator)** &middot; [Repo](https://github.com/702ron/auction-email-automation) | Cron-driven merchandising: fetches trending items, applies selection logic, fills MJML templates, delivers via Mailchimp. Dry-run previews + UTM tracking. | n8n · Airtable · MJML · Mailchimp |

---

## Web Applications & Developer Tools

| Project | What It Does | Stack |
|---------|-------------|-------|
| **[Business Metrics Dashboard](./projects/business-metrics-dashboard)** | React/TypeScript SPA, dual backends (Airtable + Supabase). Clerk performance tables, count analytics, report generation. Separate check-in app for locations. | React · TypeScript · Supabase · Vite |
| **[n8n Custom Nodes & Frontend Builder](./projects/n8n-custom-nodes)** | Open-source Plain.com GraphQL node + 47-file full-stack app that parses n8n workflows and generates interactive frontend portals. Express + React. | TypeScript · React · Express · GraphQL |
| **[n8n Plain.com Node](./projects/n8n-plain-node)** &middot; [Repo](https://github.com/702ron/n8n-plain-node) | Community node for Plain.com customer support. GraphQL integration, 6 resources, real-time event triggers. Published to npm. | TypeScript · n8n · GraphQL |

---

## Tech Stack

```
 AI/ML            GPT-4 · GPT-4 Vision · Gemini · OpenRouter · Cohere · LangChain · RAG · spaCy · scikit-learn
 Automation       n8n (228+ workflows) · RabbitMQ · Cron · Webhooks · Custom Python/Node.js
 Backend          Python · FastAPI · Django · Node.js · TypeScript · PostgreSQL · Redis · GraphQL
 Frontend         React · TypeScript · Vite · Tailwind · shadcn/ui · Chrome Extensions · MJML
 Data             Airtable (230+ bases) · Supabase · PGVector · NocoDB · Neo4j · MinIO · Google Drive
 Scraping         Selenium · Playwright · Puppeteer · Browserless.io · Firecrawl
 Payments         Stripe API (charges, refunds, webhooks)
 Infrastructure   Docker · Coolify · Nginx · Gunicorn · Self-hosted deployments
```

---

## About

I build AI-powered automation systems that bridge the gap between complex data and everyday business operations. My focus is on practical, production-ready solutions — not proofs of concept. Every project listed here runs (or has run) in a real business environment handling real transactions, real customers, and real money.

My sweet spot is taking a messy, manual business process and turning it into a reliable, automated pipeline that runs itself. Whether that's an AI agent that answers questions about your documents, a scraper that feeds pricing intelligence to your inventory system, or an n8n workflow that processes hundreds of daily transactions — I build systems that work.

**[Hire me on Upwork](https://www.upwork.com/)** 
