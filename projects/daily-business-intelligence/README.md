[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![Airtable](https://img.shields.io/badge/Airtable-Database-blue)](https://airtable.com)
[![React](https://img.shields.io/badge/React-Dashboard-61dafb)](https://react.dev)

# Automated Daily Reports — Business Intelligence at 9 AM

I engineered an automated reporting system that transforms auction sales into actionable intelligence delivered to management by 9 AM every morning. Six n8n workflows orchestrate HiBid transaction ingestion, financial calculations, HTML email generation, and real-time dashboard updates. Two-location operation with 99.2% uptime across 300+ consecutive days processes 500+ daily transactions.

## What I Built

- **Daily Sales Upload (32 nodes)** — ETL pipeline pulling HiBid transactions at 8 AM, validating data integrity, calculating financial metrics
- **Daily Numbers Email (23 nodes)** — Calculates 10+ KPIs and formats professional HTML reports with embedded charts
- **Email Builder (22 nodes)** — Templating system generating consistent, branded reports with summary tables and location comparisons
- **Import Sales Sahara (62 nodes)** — Parallel pipeline for multi-location data ingestion with separate database schemas
- **React Dashboard (daily_numbers_spa)** — Real-time metrics visualization with Tailwind CSS, 24/7 management visibility
- **Scheduled Distribution (5 nodes)** — Morning report dispatch to management inbox at 9 AM via Gmail API

## Architecture

```
HiBid API ──┐
            ├─ Daily Sales Upload (32 nodes, 8 AM)
            │    │
Airtable ──┼─ Import Sales Sahara (62 nodes)
Bases      │    │
            │    ▼
            └─ Airtable Tables (5+ bases)
                 │
                 ├─ Daily Numbers Email (23 nodes)
                 │    │
                 │    ▼
                 ├─ Email Builder (22 nodes)
                 │    │
                 │    ▼
                 └─ Morning Report (5 nodes, 9 AM)

            Parallel Output:
            • Gmail (Management Inbox)
            • React Dashboard (Real-time)
```

## Results

- **10+ KPIs** calculated daily: gross revenue, item count, average sale price, reserve met rate, buyer acquisition, return rate, location comparisons, YTD totals
- **500+ daily transactions** processed across two locations in parallel
- **99.2% uptime** over 300+ consecutive days with zero data loss
- **15 minutes saved daily** per management team member (eliminated manual data compilation)
- **10+ data integrations** — HiBid, Airtable, Gmail, Supabase, analytics
- **24/7 dashboard access** vs. daily email-only visibility
- **9 AM decision velocity** — Morning strategy reviews instead of day-end analysis
- **5+ Airtable bases** handling financial aggregation, multi-location tracking, invoice management

## Tech Stack

n8n, HiBid API, Airtable, React 18 + Vite, Tailwind CSS, Gmail API, PostgreSQL (Supabase), HTML/CSS templating

<!-- Screenshots: [Morning email report showing daily metrics table with locations, React dashboard displaying KPI cards and trend charts, Airtable Daily Auction Summary base with financial calculations] -->

---

Built by [Ron](https://github.com/702ron)
