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

## More Projects

### [Nostradamus AI — Historical Prophecy Analysis Platform](./projects/nostradamus-ai)

**Full-stack AI application analyzing Nostradamus' quatrains using NLP, machine learning, knowledge graphs, and real-time streaming.**

83 Python backend modules and 35 TypeScript frontend components. Features custom archaic French NLP processing, Neo4j knowledge graphs mapping entities across prophecies and historical events, ML-based pattern recognition with confidence scoring, 11 web scrapers (Wikipedia, Sacred Texts, Internet Archive), and real-time WebSocket analysis streaming. Production-deployed with Docker, Nginx, and JWT auth.

**Tech:** FastAPI | React | TypeScript | PostgreSQL | Neo4j | spaCy | scikit-learn | Docker | WebSockets

[View full case study &rarr;](./projects/nostradamus-ai)

---

### [Stripe Payment & Refund Automation](./projects/stripe-payment-automation)

**Reliable, multi-system payment processing with RabbitMQ message queuing, automated refunds, and comprehensive audit logging.**

Airtable triggers a return → RabbitMQ queues the event → n8n processes the void on the auction platform via Browserless → Stripe issues the refund → Airtable logs the result. Multiple entry points: 21-node n8n workflow, Python GUI (Tkinter), and JavaScript scripts. Message queuing ensures zero lost transactions even during system outages.

**Tech:** n8n | Stripe API | RabbitMQ | Airtable | Browserless.io | Python | JavaScript

[View full case study &rarr;](./projects/stripe-payment-automation)

---

### [Multi-Platform Marketplace Listing Automation](./projects/marketplace-listing-automation)

**Automated listing creation and management across HiBid, OfferUp, eBay, Amazon, and Liquidation.com.**

A 42-node n8n Lister workflow orchestrates multi-platform publishing. Selenium and Playwright scripts handle image uploads (250+ per auction). Python formatters convert retail manifests into marketplace-ready listings. Cloud-based automation via Browserless.io and Windmill enables scaling without local browser overhead. Airtable tracks listing status across all platforms.

**Tech:** n8n | Python | TypeScript | Selenium | Playwright | Browserless.io | Airtable

[View full case study &rarr;](./projects/marketplace-listing-automation)

---

### [n8n Mailchimp Automation Suite](./projects/n8n-mailchimp-automation-suite)

**Full-lifecycle email marketing automation — from customer acquisition to campaign delivery to list hygiene.**

Five interconnected n8n workflows that sync auction buyers to Mailchimp, segment by purchase behavior, generate automated campaigns with MJML templates, deliver via Mailchimp API, and clean unsubscribed contacts weekly. Airtable tracks sent emails, newsletter subscribers, and marketing performance metrics.

**Tech:** n8n | Mailchimp API | Airtable | MJML | Gmail

[View full case study &rarr;](./projects/n8n-mailchimp-automation-suite)

---

### [Auction Management Web Application](./projects/auction-management-webapp)

**Django-based platform centralizing auction creation, HiBid uploads, bidder management, and inventory operations.**

Django 5.0 application with 5 major management scripts (37K+ lines each) handling auction formatting, HiBid uploads via Selenium, void/refund processing, and Airtable synchronization. Dockerized with Gunicorn + Nginx for production deployment. Processes 1,000+ auctions monthly with integrated duplicate detection and progress tracking.

**Tech:** Django | Python | PostgreSQL | Docker | Nginx | Selenium | Airtable API | pandas

[View full case study &rarr;](./projects/auction-management-webapp)

---

### [n8n Error Monitoring & Self-Healing System](./projects/n8n-error-monitoring)

**Centralized error handling for 228+ n8n workflows with automatic retry, self-healing, and escalation.**

All production workflows feed errors to a central handler that logs to Airtable with full metadata. A daily retry job re-processes failures automatically. Specialized self-healing workflows fix common issues (location sync failures, duplicate records) without human intervention. Unresolved errors escalate via email. Maintains 85%+ auto-recovery rate across the entire automation fleet.

**Tech:** n8n | Airtable | Gmail | Error handling patterns

[View full case study &rarr;](./projects/n8n-error-monitoring)

---

### [Browser Automation Toolkit](./projects/browser-automation-toolkit)

**Production browser automation across Selenium, Playwright, Puppeteer, and Browserless.io — from local scripts to cloud-based execution.**

Battle-tested across 7+ automation projects handling auction operations. Selenium scripts process 250+ images per auction. Playwright on Windmill handles cloud-based watching and auto-bidding. Puppeteer scrapes watcher lists. Browserless.io eliminates local browser overhead entirely. Includes a self-hosted Browserless service with Docker and Python GUIs for manual override.

**Tech:** Python | Selenium | Playwright | Puppeteer | Browserless.io | TypeScript | Docker

[View full case study &rarr;](./projects/browser-automation-toolkit)

---

### [CSV & Data Pipeline Tools](./projects/csv-data-pipeline-tools)

**ETL toolkit converting retail manifests, inventory files, and auction data into marketplace-ready formats.**

A 46KB Macy's manifest converter handles multi-stage processing (XLS → CSV → Google Sheets → marketplace upload) with lot number reconciliation. A pallet grouping tool processes 81KB+ inventory files into warehouse-specific batches. Includes image-prioritized formatters for HiBid, ZPL barcode label converters for Zebra printers, and auction CSV exporters.

**Tech:** Python | pandas | Google Sheets API | Node.js | CSV/XLS Processing

[View full case study &rarr;](./projects/csv-data-pipeline-tools)

---

### [Business Metrics Dashboard](./projects/business-metrics-dashboard)

**Real-time auction analytics dashboard with clerk performance tracking, count metrics, and date-based reporting.**

React/TypeScript SPA pulling from dual backends (Airtable + Supabase). Features clerk performance tables, count-based analytics, report generation, and login authentication. Also includes a separate check-in web app for location-based operations with vehicle selection, phone verification, and payment messaging.

**Tech:** React | TypeScript | Vite | Tailwind CSS | Airtable API | Supabase

[View full case study &rarr;](./projects/business-metrics-dashboard)

---

### [n8n Custom Node & Frontend Builder](./projects/n8n-custom-nodes)

**Custom n8n ecosystem tools — from open-source community nodes to a full workflow-to-portal conversion engine.**

An open-source Plain.com GraphQL node contributed to the n8n community, plus a 47-file full-stack application that parses n8n workflows and generates interactive frontend forms and portals. The builder includes an Express backend with auth, rate limiting, and validation middleware, a React frontend for portal rendering, and a workflow parsing engine that transforms webhook and form triggers into deployable UIs.

**Tech:** TypeScript | n8n API | React | Express | GraphQL

[View full case study &rarr;](./projects/n8n-custom-nodes)

---

### [Airtable AI Chatbot — Chrome Extension](./projects/airtable-ai-chatbot)

**Chrome extension that injects an AI-powered chat interface into any Airtable page for natural language data queries.**

Manifest V3 extension with a compiled n8n Chat SDK (355KB bundle) that connects to backend AI agents via webhook. The agents (88+ workflow nodes across 5 specialized tools) can search customers, look up lot numbers, find invoices, and query inventory — all through plain English. Custom-styled to blend with Airtable's UI.

**Tech:** Chrome Extension (Manifest V3) | JavaScript | n8n | OpenAI GPT-4 | Airtable API

[View full case study &rarr;](./projects/airtable-ai-chatbot)

---

### [Job Scraper with AI Scoring](./projects/job-scraper-ai-scoring)

**Multi-platform job scraper with AI-powered relevance scoring across 8+ job boards.**

Flask web app with scrapers for Indeed, Glassdoor, LinkedIn, ZipRecruiter, Google Jobs, and more. An AI scoring module evaluates job descriptions against customizable criteria and ranks by relevance. SQLite database tracks 2MB+ of historical job data. JSearch API integration for supplemental listings.

**Tech:** Python | Flask | SQLite | OpenAI | Poetry

[View full case study &rarr;](./projects/job-scraper-ai-scoring)

---

## Standalone Repos

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
