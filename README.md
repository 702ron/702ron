# AI & Automation Engineering Portfolio

Building intelligent systems that solve real business problems — from AI agents and RAG pipelines to full-scale business automation across 228+ n8n workflows, 230+ Airtable bases, and dozens of custom scripts.

---

## What I Do

I design and build production automation systems at the intersection of AI, data, and business operations. My work spans the full stack: LLM-powered agents that reason about business data, n8n workflows that orchestrate complex multi-step processes, web scrapers that feed pricing intelligence, and Airtable ecosystems that run entire businesses. Everything I build runs in production — not demos.

**By the numbers:**
- **228+** n8n workflows built (79 in production daily)
- **230+** Airtable bases powering multi-location operations
- **165+** automation scripts and custom tools
- **4+ years** of continuous iteration on live business systems

---

## AI & Intelligent Agents

### [RAG AI Agent — Document Intelligence System](./projects/n8n-rag-ai-agent)

54-node n8n workflow with three integrated subsystems: a conversational AI agent with four specialized tools (vector search, document listing, content retrieval, tabular queries), an automated document ingestion pipeline triggered by Google Drive, and a garbage collection system that keeps the knowledge base current. Supports PDF, Excel, CSV, and Word with PGVector semantic search and Cohere re-ranking.

**Tech:** n8n | OpenAI GPT-4 | PGVector | Cohere Rerank | PostgreSQL | Google Drive | LangChain

---

### [AI Label Designer](./projects/ai-label-designer) | [Live Demo](https://labelwizard.702market.com/) | [GitHub](https://github.com/702ron/1932-label-wizard)

Full-stack whiskey barrel label creator with a 4-step wizard: text input, AI logo generation, AI background creation, real-time fine-tuning, and photorealistic bottle mockup. React frontend, FastAPI backend, OpenRouter and Google Gemini for image generation, Redis caching, PostgreSQL persistence, MinIO object storage.

**Tech:** React | FastAPI | TypeScript | Python | OpenRouter | Google Gemini | Redis | PostgreSQL | MinIO

---

### [Airtable Chat Support Agent](./projects/airtable-chat-agent) | [GitHub](https://github.com/702ron/airtable-chat-support-agent)

AI-powered natural language interface for business data. Converts natural language queries into structured Airtable lookups across Inventory, Sales, and Returns tables. Features barcode image recognition, session-aware conversations with PostgreSQL chat memory, and dual frontend options (Open WebUI or custom interface).

**Tech:** n8n | OpenAI GPT-4 | Airtable | PostgreSQL | Open WebUI

---

### [Airtable AI Chatbot — Chrome Extension](./projects/airtable-ai-chatbot)

Chrome Manifest V3 extension that injects an AI chat interface into any Airtable page. A compiled n8n Chat SDK (355KB bundle) connects to backend AI agents via webhook. The agents (88+ workflow nodes across 5 specialized tools) search customers, look up lot numbers, find invoices, and query inventory — all through plain English.

**Tech:** Chrome Extension (Manifest V3) | JavaScript | n8n | OpenAI GPT-4 | Airtable API

---

### [AI Email Labeler & Assistant](./projects/ai-email-labeler)

An 18-node n8n workflow that automatically classifies incoming emails using GPT-4 and applies smart Gmail labels in real-time. Paired with the Gmail Agent V2 (22 nodes) that reads full email threads, summarizes conversations, and drafts intelligent responses. Running in production daily.

**Tech:** n8n | OpenAI GPT-4 | Gmail API | Google Sheets

---

### [AI Resume Parser & Applicant Tracker](./projects/resume-parser) | [GitHub](https://github.com/702ron/resume-parser-airtable)

Automated recruitment pipeline: monitors Gmail for applications, extracts resume data with GPT-4 (contact info, work history, highlights across 8 fields), stores files in Google Drive, and organizes applicants in Airtable. Customizable for LinkedIn, Indeed, and direct application sources.

**Tech:** n8n | OpenAI GPT-4 | Gmail | Google Drive | Airtable

---

### [Nostradamus AI — Historical Prophecy Analysis Platform](./projects/nostradamus-ai)

Full-stack AI application: 83 Python backend modules and 35 TypeScript frontend components. Custom archaic French NLP processing, Neo4j knowledge graphs mapping entities across prophecies and historical events, ML-based pattern recognition with confidence scoring, 11 web scrapers, and real-time WebSocket streaming. Production-deployed with Docker and Nginx.

**Tech:** FastAPI | React | TypeScript | PostgreSQL | Neo4j | spaCy | scikit-learn | Docker | WebSockets

---

### [Job Scraper with AI Scoring](./projects/job-scraper-ai-scoring)

Flask web app scraping 8+ job boards (Indeed, Glassdoor, LinkedIn, ZipRecruiter, Google Jobs) with an AI scoring module that evaluates descriptions against customizable criteria and ranks by relevance. SQLite database tracks 2MB+ of historical job data.

**Tech:** Python | Flask | SQLite | OpenAI | Poetry

---

## Business Automation & Operations

### [HiBid Auction Automation Suite](./projects/hibid-auction-automation)

Production system handling thousands of monthly auctions. The HiBid Lister (42 nodes) automates multi-platform listing. The Watcher (25 nodes) monitors auctions in real-time and feeds data to Airtable. Custom Selenium/Playwright scripts handle bid placement and user scraping. Stripe integration processes payments and refunds via RabbitMQ message queuing.

**Tech:** n8n | Airtable | Selenium | Playwright | Browserless.io | Stripe | RabbitMQ | Mailchimp

---

### [Airtable Operations Platform](./projects/airtable-operations-platform)

Enterprise-grade Airtable ecosystem: 230+ bases, 50+ active in daily operations, 4+ years of continuous development. Manages inventory, finance, sales, returns, HR, and marketplace integrations across two physical locations. Includes 426+ Airtable node uses across n8n workflows, custom AI agents, and automated backup systems.

**Tech:** Airtable | n8n | OpenAI | JavaScript (Browser Extension) | Supabase | Stripe | Mailchimp

---

### [Daily Business Intelligence Pipeline](./projects/daily-business-intelligence)

A network of 6 interconnected n8n workflows (up to 62 nodes each) that pull sales data from HiBid, process transactions, calculate KPIs (revenue, item counts, average sale price, buyer metrics), cross-reference inventory and returns, and deliver formatted HTML reports to management at 9AM daily. Companion React/Vite dashboard for real-time access.

**Tech:** n8n | Airtable | React | Vite | Tailwind CSS | Gmail | HTML Email

---

### [Stripe Payment & Refund Automation](./projects/stripe-payment-automation)

Airtable triggers a return → RabbitMQ queues the event → n8n processes the void on the auction platform via Browserless → Stripe issues the refund → Airtable logs the result. Multiple entry points: 21-node n8n workflow, Python GUI (Tkinter), and JavaScript scripts. Message queuing ensures zero lost transactions.

**Tech:** n8n | Stripe API | RabbitMQ | Airtable | Browserless.io | Python | JavaScript

---

### [Refund Returns Processing System](./projects/refund-returns-system) | [GitHub](https://github.com/702ron/refund-returns-processing)

End-to-end returns workflow with 7-step automated processing, 6 return type categories, and multi-location support. Uses RabbitMQ for reliable message queuing, browserless automation for external system voids, and Stripe API for refund handling. Idempotent processing with comprehensive audit logging.

**Tech:** n8n | RabbitMQ | Stripe API | Airtable | Browserless

---

### [Auction Management Web Application](./projects/auction-management-webapp)

Django 5.0 platform with 5 major management scripts (37K+ lines each) handling auction formatting, HiBid uploads via Selenium, void/refund processing, and Airtable synchronization. Dockerized with Gunicorn + Nginx for production. Processes 1,000+ auctions monthly.

**Tech:** Django | Python | PostgreSQL | Docker | Nginx | Selenium | Airtable API | pandas

---

### [n8n Error Monitoring & Self-Healing System](./projects/n8n-error-monitoring)

Centralized error handling for 228+ n8n workflows. All production workflows feed errors to a central handler → Airtable logs with metadata → daily retry job re-processes failures → self-healing workflows auto-fix common issues → unresolved errors escalate via email. 85%+ auto-recovery rate.

**Tech:** n8n | Airtable | Gmail | Error handling patterns

---

## Web Scraping & Data Pipelines

### [Retail Product Scraper Suite](./projects/retail-product-scraper)

Modular scraping suite: Macy's (full catalog with Selenium), Lowe's (API + barcode + Amazon/CamelCamelCamel integration), Kohl's (manifest downloader, 4 versions), Amazon (ASIN/UPC/FNSKU tools), and Google Trends. Feeds into Airtable for automated pricing decisions. Both standalone Python scripts and n8n workflow integrations.

**Tech:** Python | Selenium | Playwright | Requests | n8n | Airtable | REST APIs

---

### [Product Info Lookup API](./projects/product-info-lookup) | [GitHub](https://github.com/702ron/product-info-lookup)

Universal product data retrieval across Amazon, Walmart, Target, and Home Depot. Auto-detects identifier types (ASIN, UPC, FNSKU, URL, LOT), queries 6 third-party APIs, caches results in NocoDB, and applies AI-powered categorization via Google Gemini and GPT-4. Firecrawl fallback for scraping.

**Tech:** n8n | NocoDB | Google Gemini | OpenAI GPT-4 | Firecrawl | Airtable

---

### [CSV & Data Pipeline Tools](./projects/csv-data-pipeline-tools)

ETL toolkit: a 46KB Macy's manifest converter (XLS → CSV → Google Sheets → marketplace), pallet grouping for 81KB+ inventory files, image-prioritized formatters for HiBid, ZPL barcode label converters for Zebra printers, and auction CSV exporters.

**Tech:** Python | pandas | Google Sheets API | Node.js | CSV/XLS Processing

---

### [Browser Automation Toolkit](./projects/browser-automation-toolkit)

Production browser automation across 4 frameworks: Selenium scripts processing 250+ images per auction, Playwright on Windmill for cloud watching and auto-bidding, Puppeteer for watcher list scraping, and Browserless.io for zero-overhead cloud execution. Includes a self-hosted Browserless service with Docker.

**Tech:** Python | Selenium | Playwright | Puppeteer | Browserless.io | TypeScript | Docker

---

## Marketing & E-Commerce

### [Multi-Platform Marketplace Listing Automation](./projects/marketplace-listing-automation)

Automated listing across HiBid, OfferUp, eBay, Amazon, and Liquidation.com. A 42-node n8n Lister orchestrates multi-platform publishing. Selenium and Playwright handle image uploads (250+ per auction). Python formatters convert retail manifests into marketplace-ready listings. Airtable tracks status across all platforms.

**Tech:** n8n | Python | TypeScript | Selenium | Playwright | Browserless.io | Airtable

---

### [n8n Mailchimp Automation Suite](./projects/n8n-mailchimp-automation-suite)

Five interconnected n8n workflows: sync auction buyers to Mailchimp, segment by purchase behavior, generate campaigns with MJML templates, deliver via Mailchimp API, and clean unsubscribed contacts weekly. Airtable tracks sent emails, subscribers, and performance.

**Tech:** n8n | Mailchimp API | Airtable | MJML | Gmail

---

### [Email Campaign Generator](./projects/email-campaign-generator) | [GitHub](https://github.com/702ron/auction-email-automation)

Cron-driven merchandising automation: fetches trending items from Airtable, applies selection logic and deduplication, fills responsive MJML templates, and delivers via Mailchimp. Features dry-run previews, UTM tracking, and error notifications.

**Tech:** n8n | Airtable | MJML | Mailchimp | Gmail

---

## Web Applications & Developer Tools

### [Business Metrics Dashboard](./projects/business-metrics-dashboard)

React/TypeScript SPA with dual backends (Airtable + Supabase). Features clerk performance tables, count-based analytics, report generation, and date-based filtering. Also includes a separate check-in web app for location-based operations with vehicle selection, phone verification, and payment messaging.

**Tech:** React | TypeScript | Vite | Tailwind CSS | Airtable API | Supabase

---

### [n8n Custom Node & Frontend Builder](./projects/n8n-custom-nodes)

An open-source Plain.com GraphQL node for the n8n community, plus a 47-file full-stack application that parses n8n workflows and generates interactive frontend forms and portals. Express backend with auth, rate limiting, and validation; React frontend for portal rendering; workflow parsing engine for webhook and form trigger transformation.

**Tech:** TypeScript | n8n API | React | Express | GraphQL

---

### [n8n Plain.com Integration Node](./projects/n8n-plain-node) | [GitHub](https://github.com/702ron/n8n-plain-node)

Open-source n8n community node for Plain.com customer support platform. GraphQL API integration covering 6 resources with real-time event triggers. Published to npm.

**Tech:** TypeScript | n8n | GraphQL

---

## Tech Stack

| Category | Technologies |
|----------|-------------|
| **AI/ML** | OpenAI GPT-4, GPT-4 Vision, Google Gemini, OpenRouter, Cohere, LangChain, RAG, Multi-Agent Systems, Prompt Engineering |
| **Automation** | n8n (228+ workflows), Custom Python/Node.js scripts, Webhook integrations, RabbitMQ, Cron scheduling |
| **Backend** | Python, FastAPI, Django, Node.js, TypeScript, PostgreSQL, Redis, REST APIs, GraphQL |
| **Frontend** | React, TypeScript, Vite, Tailwind CSS, shadcn/ui, Chrome Extensions, MJML Email Templates |
| **Data** | Airtable (230+ bases), Supabase, PGVector, NocoDB, Neo4j, MinIO, Google Drive |
| **Scraping** | Selenium, Playwright, Puppeteer, Browserless.io, Firecrawl, Requests |
| **Payments** | Stripe API (payments, refunds, webhooks) |
| **Infrastructure** | Docker, Coolify, Nginx, Gunicorn, Self-hosted deployments |

---

## About

I build AI-powered automation systems that bridge the gap between complex data and everyday business operations. My focus is on practical, production-ready solutions — not proofs of concept. Every project listed here runs (or has run) in a real business environment handling real transactions, real customers, and real money.

My sweet spot is taking a messy, manual business process and turning it into a reliable, automated pipeline that runs itself. Whether that's an AI agent that answers questions about your documents, a scraper that feeds pricing intelligence to your inventory system, or an n8n workflow that processes hundreds of daily transactions across multiple locations — I build systems that work.

---

*Open to freelance and contract work. [Reach out on Upwork](https://www.upwork.com/) or [email me](mailto:ron@702auctions.com).*
