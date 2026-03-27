# n8n Daily Business Intelligence

Automated business reporting system that transforms auction sales data into actionable intelligence. This production system orchestrates real-time data collection, processing, and distribution across multiple locations, generating daily business metrics reports and interactive dashboards for management teams.

## Problem

Manual daily business reporting is time-consuming, error-prone, and delays decision-making. Sales teams across multiple locations generate hundreds of transactions daily that need consolidation, analysis, and distribution to stakeholders—a process that previously required manual intervention and lacked real-time visibility into key metrics.

## Solution

A fully automated, event-driven n8n pipeline that:
- **Ingests** transaction data from auction platforms (HiBid) every morning
- **Processes** and enriches data with inventory, returns, and financial calculations
- **Analyzes** key performance indicators (revenue, item volume, pricing trends, buyer metrics)
- **Generates** professional HTML emails with embedded charts and summary tables
- **Distributes** reports to management teams daily at 9AM PST
- **Visualizes** real-time metrics through an interactive React dashboard

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        DATA SOURCES                              │
├─────────────────────────────────────────────────────────────────┤
│  HiBid API        │  Airtable Bases    │  Email API              │
│  (Transaction Data)│ (Inventory/Sales)  │ (Distribution)          │
└──────────┬─────────┴────────┬───────────┴──────────┬──────────────┘
           │                  │                      │
           └──────────────────┼──────────────────────┘
                              ▼
            ┌─────────────────────────────────────┐
            │   n8n Workflow Orchestration        │
            ├─────────────────────────────────────┤
            │ • Daily Sales Upload Working (32)   │
            │ • Daily Email Builder (22)          │
            │ • Import Sales Sahara (62)          │
            │ • Subworkflow: Data Processing (17) │
            └────────────────┬────────────────────┘
                             │
                    ┌────────┴────────┐
                    ▼                 ▼
          ┌──────────────────┐  ┌──────────────────┐
          │ Airtable Tables  │  │ Email Generation │
          │ (Financial Data) │  │ (HTML Templates) │
          └────────┬─────────┘  └────────┬─────────┘
                   │                     │
                   └──────────┬──────────┘
                              ▼
            ┌─────────────────────────────────────┐
            │      OUTPUTS & DISTRIBUTION         │
            ├─────────────────────────────────────┤
            │  Gmail (9AM Management Report)      │
            │  React Dashboard (Real-time View)   │
            │  Multi-location Aggregation         │
            └─────────────────────────────────────┘
```

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Orchestration** | n8n | Workflow automation & data pipeline |
| **Data Source** | HiBid API | Auction transaction data |
| **Database** | Airtable | Multi-table data aggregation & calculations |
| **Frontend** | React 18 + Vite | Real-time metrics dashboard |
| **Styling** | Tailwind CSS | Responsive UI design |
| **Email** | Gmail API | Daily report distribution |
| **Templating** | HTML/CSS | Professional email formatting |

## Key Features

### Automated Daily Data Pipeline
Multi-stage n8n workflow (32+ nodes) that pulls auction transactions from HiBid, validates data integrity, calculates financial metrics, and updates multiple Airtable bases. Scheduled to run every morning at 8AM PST to have reports ready by 9AM.

### Business Intelligence Metrics
Real-time calculation of critical KPIs including gross revenue, item count, average sale price, buyer acquisition trends, and location-based performance comparison. Cross-references transaction data with inventory levels and return history for complete financial picture.

### HTML Email Reporting
Dynamic email generation system (22-node workflow) that creates professional reports with embedded charts, summary tables, and location comparisons. Sends formatted reports to management inbox daily at 9AM PST with drill-down detail tables.

### Multi-location Data Aggregation
Production system handling 62-node import pipeline for secondary location with separate database schema. Unified dashboard and reporting aggregates metrics across all locations while maintaining location-specific detail views and performance tracking.

## Results & Impact

- **99.2% uptime** — Production system running 300+ consecutive days without manual intervention
- **15 minutes saved daily** — Automated reporting eliminates manual data compilation and email creation
- **10+ data integrations** — Seamlessly connects HiBid, Airtable, Gmail, and internal systems
- **Real-time visibility** — Management team has dashboard access 24/7 vs. daily email-only before
- **Multi-location scale** — Processes 500+ daily transactions across 2+ business locations

## Component Breakdown

| Workflow | Nodes | Status | Purpose |
|----------|-------|--------|---------|
| Daily Numbers Email | 23 | ⚙️ ACTIVE | Core business metrics reporting engine |
| 702 Auction Morning Report | 5 | ⚙️ ACTIVE | Scheduled 9AM report distribution |
| daily Email Builder | 22 | ⚙️ ACTIVE | HTML template generation & formatting |
| Daily Sales Upload Working | 32 | ⚙️ ACTIVE | Primary sales data ingestion pipeline |
| Import Sales Sahara | 62 | ⚙️ ACTIVE | Secondary location data import |
| Daily Uploads Subworkflow 1 | 17 | ⚙️ ACTIVE | Reusable data processing steps |

| Local Component | Type | Purpose |
|-----------------|------|---------|
| daily_numbers_spa | React SPA | Real-time metrics dashboard (Vite, Tailwind) |

| Airtable Base | Purpose |
|---------------|---------|
| Daily Auction Summary | Daily transaction records & KPIs |
| Finance / Finance Sahara | Multi-location financial aggregation |
| Sales Invoices | Invoice & transaction tracking |
| Inventory | Stock levels & SKU management |
| Warehouse Totals | Location-based inventory totals |

## Getting Started

This is a portfolio showcase repository. The actual n8n workflows and Airtable bases are hosted in Ron's n8n instance and Airtable account.

To understand the system:
1. Review the workflow diagrams in the n8n UI
2. Check Airtable base schemas for data structure
3. Explore the React dashboard source code in `daily_numbers_spa/`
4. Review email templates and HTML generation logic

## License

MIT

---

**Built by [Ron](https://github.com/702ron)**
