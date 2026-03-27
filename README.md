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

## Featured Projects

### [RAG AI Agent — Document Intelligence System](./projects/n8n-rag-ai-agent)

**Chat with your documents using natural language. Supports PDF, Excel, CSV, and Word with automatic ingestion, vector search, and intelligent re-ranking.**

54-node n8n workflow with three integrated subsystems: a conversational AI agent with four specialized tools (vector search, document listing, content retrieval, tabular queries), an automated document ingestion pipeline triggered by Google Drive, and a garbage collection system that keeps the knowledge base current. Uses PGVector for semantic search and Cohere for result re-ranking.

**Tech:** n8n | OpenAI GPT-4 | PGVector | Cohere Rerank | PostgreSQL | Google Drive | LangChain

[View full case study &rarr;](./projects/n8n-rag-ai-agent)

---

### [HiBid Auction Automation Suite](./projects/hibid-auction-automation)

**End-to-end automation of multi-location auction operations — listing, monitoring, bidding, payments, and inventory management.**

A production system handling thousands of monthly auctions with minimal manual intervention. The HiBid Lister (42 nodes) automates multi-platform listing. The Watcher (25 nodes) monitors auctions in real-time and feeds data to Airtable. Custom Selenium/Playwright scripts handle bid placement and user scraping. Stripe integration processes payments and refunds automatically via RabbitMQ message queuing.

**Tech:** n8n | Airtable | Selenium | Playwright | Browserless.io | Stripe | RabbitMQ | Mailchimp

[View full case study &rarr;](./projects/hibid-auction-automation)

---

### [AI Email Labeler & Assistant](./projects/ai-email-labeler)

**AI-powered email classification, labeling, and response drafting for Gmail — running in production daily.**

An 18-node n8n workflow that automatically classifies incoming emails using GPT-4 and applies smart Gmail labels in real-time. Paired with the Gmail Agent V2 (22 nodes) that reads full email threads, summarizes conversations, and drafts intelligent responses. Handles business categories like orders, returns, vendor communications, and customer inquiries.

**Tech:** n8n | OpenAI GPT-4 | Gmail API | Google Sheets

[View full case study &rarr;](./projects/ai-email-labeler)

---

### [Daily Business Intelligence Pipeline](./projects/daily-business-intelligence)

**Automated KPI reporting across multiple business locations — from raw transaction data to formatted executive emails and a real-time dashboard.**

A network of 6 interconnected n8n workflows (up to 62 nodes each) that pull sales data from HiBid, process transactions, calculate KPIs (revenue, item counts, average sale price, buyer metrics), cross-reference inventory and returns, and deliver formatted HTML reports to management at 9AM daily. A companion React/Vite dashboard provides real-time access.

**Tech:** n8n | Airtable | React | Vite | Tailwind CSS | Gmail | HTML Email

[View full case study &rarr;](./projects/daily-business-intelligence)

---

### [Retail Product Scraper Suite](./projects/retail-product-scraper)

**Multi-retailer web scraping toolkit for pricing intelligence and product data extraction at scale.**

Modular scraping suite covering Macy's (full catalog scraper with Selenium), Lowe's (API + barcode lookup + Amazon/CamelCamelCamel integration), Kohl's (manifest downloader across 4 versions), Amazon (ASIN/UPC/FNSKU lookup tools), and Google Trends. Feeds into Airtable-based inventory management for automated pricing decisions. Includes both standalone Python scripts and n8n workflow integrations.

**Tech:** Python | Selenium | Playwright | Requests | n8n | Airtable | REST APIs

[View full case study &rarr;](./projects/retail-product-scraper)

---

### [Airtable Operations Platform](./projects/airtable-operations-platform)

**Enterprise-grade Airtable ecosystem running a multi-location auction and retail business — 230+ bases, 50+ active in daily operations.**

A 4+ year, continuously evolving Airtable platform managing inventory, finance, sales, returns, HR, marketplace integrations, and AI-driven workflows. Includes a custom browser extension for AI chat within Airtable, multiple AI agents for natural language querying, and 426+ Airtable node uses across n8n workflows. Supports two physical locations with unified reporting and automated backups.

**Tech:** Airtable | n8n | OpenAI | JavaScript (Browser Extension) | Supabase | Stripe | Mailchimp

[View full case study &rarr;](./projects/airtable-operations-platform)

---

## Additional Projects

### [AI Label Designer](https://github.com/702ron/1932-label-wizard) | [Live Demo](https://labelwizard.702market.com/)

Custom whiskey label creator with AI-powered image generation. Full-stack web application featuring a 4-step wizard with AI logo generation, custom background creation, real-time fine-tuning, and photorealistic bottle mockups.

**Tech:** React | FastAPI | TypeScript | Python | OpenRouter | Google Gemini | Redis | PostgreSQL | MinIO

---

### [Airtable Chat Support Agent](https://github.com/702ron/airtable-chat-support-agent)

AI-powered natural language interface for business data. Converts natural language queries into structured Airtable lookups with multi-table querying, barcode image recognition, and session-aware conversations.

**Tech:** n8n | OpenAI GPT-4 | Airtable | PostgreSQL | Open WebUI

---

### [Product Info Lookup API](https://github.com/702ron/product-info-lookup)

Universal product data retrieval with multi-retailer integration. Automatically detects identifier types (ASIN, UPC, FNSKU, URL, LOT) and retrieves product data from Amazon, Walmart, Target, and Home Depot with intelligent caching and AI-powered categorization.

**Tech:** n8n | NocoDB | Google Gemini | OpenAI GPT-4 | Firecrawl | Airtable

---

### [Refund Returns Processing System](https://github.com/702ron/refund-returns-processing)

Automated returns workflow with Stripe refunds and message queuing. End-to-end system triggered from Airtable using RabbitMQ for reliable processing, browserless automation for external system voids, and Stripe API for refund handling.

**Tech:** n8n | RabbitMQ | Stripe API | Airtable | Browserless

---

### [AI Resume Parser & Applicant Tracker](https://github.com/702ron/resume-parser-airtable)

Automated recruitment pipeline. Monitors Gmail for job applications, extracts resume data using GPT-4 (contact info, work history, highlights), stores files in Google Drive, and organizes applicants in Airtable.

**Tech:** n8n | OpenAI GPT-4 | Gmail | Google Drive | Airtable

---

### [Automated Email Campaign Generator](https://github.com/702ron/auction-email-automation)

Cron-driven email automation that fetches trending items from Airtable, applies selection logic and de-duplication, fills responsive MJML templates, and delivers campaigns via Mailchimp with dry-run previews, UTM tracking, and error notifications.

**Tech:** n8n | Airtable | MJML | Mailchimp | Gmail

---

### [n8n Plain.com Integration Node](https://github.com/702ron/n8n-plain-node)

Custom n8n community node for Plain.com GraphQL API integration. Open-source contribution to the n8n ecosystem.

**Tech:** TypeScript | n8n | GraphQL

---

## Tech Stack

| Category | Technologies |
|----------|-------------|
| **AI/ML** | OpenAI GPT-4, GPT-4 Vision, Google Gemini, OpenRouter, Cohere, LangChain, RAG, Multi-Agent Systems, Prompt Engineering |
| **Automation** | n8n (228+ workflows), Custom Python/Node.js scripts, Webhook integrations, RabbitMQ, Cron scheduling |
| **Backend** | Python, FastAPI, Node.js, TypeScript, PostgreSQL, Redis, REST APIs, GraphQL |
| **Frontend** | React, TypeScript, Vite, Tailwind CSS, shadcn/ui, MJML Email Templates |
| **Data** | Airtable (230+ bases), Supabase, PGVector, NocoDB, MinIO, Google Drive |
| **Scraping** | Selenium, Playwright, Puppeteer, Browserless.io, Firecrawl, Requests |
| **Payments** | Stripe API (payments, refunds, webhooks) |
| **Infrastructure** | Docker, Coolify, Self-hosted deployments, GitHub Actions |

---

## About

I build AI-powered automation systems that bridge the gap between complex data and everyday business operations. My focus is on practical, production-ready solutions — not proofs of concept. Every project listed here runs (or has run) in a real business environment handling real transactions, real customers, and real money.

My sweet spot is taking a messy, manual business process and turning it into a reliable, automated pipeline that runs itself. Whether that's an AI agent that answers questions about your documents, a scraper that feeds pricing intelligence to your inventory system, or an n8n workflow that processes hundreds of daily transactions across multiple locations — I build systems that work.

---

*Open to freelance and contract work. [Reach out on Upwork](https://www.upwork.com/) or [email me](mailto:ron@702auctions.com).*
