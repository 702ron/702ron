[![Airtable](https://img.shields.io/badge/Airtable-Database-blue)](https://airtable.com)
[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![Stripe](https://img.shields.io/badge/Stripe-Payments-brightgreen)](https://stripe.com)
[![MIT License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

# Airtable Operations Platform — Enterprise Multi-Location Business System

A comprehensive, enterprise-grade Airtable ecosystem powering multi-location auction and retail operations. This system manages 230+ interconnected bases handling inventory, finance, sales, HR, marketplace integrations, and AI-driven workflows across a complex, fast-moving business requiring real-time visibility and automation at scale. Processes 4,000+ auctions monthly, manages 50+ active bases daily, maintains 4+ years of historical data with 20+ version controls on critical bases.

## What I Built

**Custom operating system for auction business** integrating 230+ Airtable bases with 426+ n8n node connections, 3+ AI agents, custom browser extension, and complete multi-location infrastructure:

- **Inventory & Warehouse Management** — Centralized stock tracking across 2 physical locations and multiple online channels; main Inventory base linked to 20+ historical backups, Pull Lists, and Warehouse Totals
- **Finance & Multi-Location Accounting** — Dual-location finance system tracking revenue across auction channels, consignment deals, and retail sales; built-in audit trails, 4+ years of financial history
- **Sales & CRM Layer** — Unified sales infrastructure combining Sales Invoices, Sales CRM, Customer management, linked to marketplace listings and order fulfillment
- **Returns & Quality Assurance** — Specialized 4-base system (Returns, Return Analytics, Return Inspection, Return Archive) with automated refund processing and audit trails
- **Marketplace Integration** — Five parallel marketplace systems (Hibid, OfferUp, Amazon, Liquidation, eBay) with dedicated formatters, lot watchers, and real-time sync
- **Human Resources & Operations** — Employee management spanning hours tracking, onboarding, company directory (702 Employees base), plus Ticket Management and Project Management
- **AI Agents & Extensions** — Custom chatbot browser extension + 3+ AI agents (general lookup, customer lookup, invoice lookup, lot lookup) querying Airtable in real-time

## Scale Metrics

| Metric | Value | Impact |
|--------|-------|--------|
| **Total Bases** | 230+ | Organized by functional layer (Inventory, Finance, Sales, HR, Marketing, AI) |
| **Active Daily Bases** | 50+ | Bases with daily read/write operations |
| **Years of Data** | 4+ | Historical backups from 2021; enables trend analysis and audit compliance |
| **Physical Locations** | 2 | Sahara and Sunrise; separate instances with unified reporting |
| **n8n Airtable Nodes** | 426+ | Integrations across 20+ active workflows |
| **Backup Versions** | 20+ per base | Critical bases (Inventory, Finance, Sales) with complete version history |
| **Marketplace Platforms** | 5+ | Hibid, OfferUp, Amazon Pallets, Liquidation.com, eBay |
| **AI Agents** | 3+ | Customer lookup, Invoice lookup, Lot number lookup, General Airtable agent |
| **Custom Extensions** | 1 | Browser chatbot overlay for Airtable; JavaScript-based, self-hosted |
| **Monthly Transactions** | 4,000–5,000 | Auctions created, tracked, and managed |
| **Records Managed** | 100,000+ | Cumulative across all 230 bases |

## Architecture Map

```
┌──────────────────────────────────────────────────────────────────┐
│          AIRTABLE OPERATIONS PLATFORM ARCHITECTURE               │
└──────────────────────────────────────────────────────────────────┘

┌────────────────────┐  ┌────────────────────┐  ┌────────────────────┐
│ INVENTORY LAYER    │  │ FINANCE LAYER      │  │ SALES LAYER        │
├────────────────────┤  ├────────────────────┤  ├────────────────────┤
│ • Inventory (Main) │  │ • Finance (Main)   │  │ • Sales Invoices   │
│ • Inventory Dev    │  │ • Finance Sahara   │  │ • Sales CRM        │
│ • 20+ Backups      │  │ • Invoice Lookup   │  │ • Sales Archive    │
│ • Warehouse Totals │  │ • Financial Report │  │ • Invoices (Search)│
│ • Pull Lists       │  │ • Stripe Integr.   │  │ • Order History    │
│ • Lot Tracking     │  └────────────────────┘  └────────────────────┘
│ • Source Tracker   │
└────────────────────┘

┌────────────────────┐  ┌────────────────────┐  ┌────────────────────┐
│ OPERATIONS LAYER   │  │ HR & PEOPLE LAYER  │  │ MARKETPLACE LAYER  │
├────────────────────┤  ├────────────────────┤  ├────────────────────┤
│ • Order Pickup     │  │ • Employee Hours   │  │ • Hibid Formatter  │
│ • Returns (4)      │  │ • Emp. Purchase    │  │ • OfferUp (2x)     │
│ • Daily Auction    │  │ • Emp. Onboard     │  │ • Amazon Pallets   │
│ • Appointments     │  │ • 702 Employees    │  │ • Liquidation.com  │
│ • Salvage (2)      │  │ • Ticket Mgmt      │  │ • eBay Integration │
│ • Project Mgmt     │  │ • Wholesale Deals  │  │ • Lot Watchers     │
│ • Booth Numbers    │  │ • Customer Lists   │  └────────────────────┘
└────────────────────┘  └────────────────────┘

┌────────────────────┐  ┌────────────────────┐
│ MARKETING LAYER    │  │ AI & AUTOMATION    │
├────────────────────┤  ├────────────────────┤
│ • Newsletter Sync  │  │ • Chatbot Ext.     │
│ • Social Media Pl. │  │ • 426 n8n Nodes    │
│ • Marketing Report │  │ • AI Agents (3+)   │
│ • Survey Data      │  │ • Webhook Endpoints│
│ • Email Analytics  │  │ • Lookup Services  │
└────────────────────┘  └────────────────────┘

         ↓ ALL SYSTEMS CONNECTED VIA ↓

    n8n Hub + Custom Scripts + Browser Extension
```

## System Modules Breakdown

### 1. Inventory & Warehouse Management
**Primary System**: Main Inventory base with 10,000+ SKU records, linked to Warehouse Totals, Pull Lists, and 20+ historical backup versions. Each location (Sahara/Sunrise) maintains separate Inventory instances for operational autonomy while Master Inventory aggregates data for unified reporting. Backup strategy ensures zero data loss—critical base snapshots taken daily to Supabase for rapid recovery. Pull Lists generated hourly based on order pipeline, enabling floor staff to physically gather items.

### 2. Finance & Multi-Location Accounting
**Dual-Location Finance System**: Main Finance base tracks primary location revenue (Sunrise); Finance Sahara tracks secondary location independently. Both sync via n8n to unified Finance reporting base for management dashboards. Integrated with Stripe for payment processing and refund automation. Invoice Lookup base provides rapid transaction search by customer, date range, or amount. Built-in audit trails and 4+ years of historical data enable regulatory compliance, variance analysis, and financial forecasting.

### 3. Sales & Customer Relationship Management
**Unified Sales Infrastructure**: Sales Invoices base combines all transaction types (auction wins, retail sales, consignment settlements). Sales CRM tracks customer interactions, purchase history, and repeat buyer metrics. Customer Lists base segments buyers by value tier, enabling targeted Mailchimp campaigns. Linked directly to marketplace listings and inventory, enabling one-click invoice generation, customer history lookup, and cross-sell analysis.

### 4. Returns & Quality Assurance
**Specialized 4-Base System**: Returns base tracks inbound return requests with reason codes and condition assessments. Return Inspection base captures detailed QA findings (damage, missing parts, condition verification). Return Analytics rollup base calculates return rate by location, product category, and seller—enabling process improvements. Return Archive preserves historical data for trend analysis (product reliability, seasonal patterns). Integrates with Finance for automatic reconciliation and Stripe for refund generation.

### 5. Marketplace Integration & Omnichannel
**Five Parallel Marketplace Systems**: Each platform (Hibid, OfferUp, Amazon Pallets, Liquidation.com, eBay) has dedicated formatter base (data standardization), lot watcher base (price tracking and win notifications), and inventory link (deduction on sale). n8n orchestrates cross-platform inventory sync—when item sells on OfferUp, inventory decrements on all other platforms instantly. Prevent overselling and duplicate listings through centralized inventory management.

### 6. Human Resources & People Operations
**Employee Management Suite**: Employee Hours base tracks shifts, overtime, and payroll integration. Employee Purchase program base manages employee discounts and benefits. Employee Onboarding base tracks hiring workflows and training completion. 702 Employees base serves as company directory with role, contact, and department info. Ticket Management system routes employee requests (IT issues, supplies, facility requests) with automated escalation. Wholesale Deals CRM manages B2B relationships and partner agreements.

### 7. Marketing & Communications
**Newsletter & Campaign Management**: Newsletter Sync base integrates with Mailchimp for subscriber management and campaign tracking. Social Media Planning base schedules posts and tracks engagement. Marketing Reports base aggregates campaign metrics (open rates, click rates, ROI by campaign). Survey Data base collects and analyzes customer feedback. Email Analytics dashboard measures outreach effectiveness across all channels.

### 8. AI Agents & Advanced Automation
**Airtable Agent Suite**: General-purpose lookup service queries any base and field (e.g., "Show me all returns from March"). Customer Lookup Agent returns instant customer history, purchase records, contact info. Invoice Lookup Agent searches invoices by customer/date/amount with drill-down to line item detail. Lot Number Lookup Agent provides real-time inventory visibility tied to auction lot numbers. All agents leverage 426+ n8n nodes connecting Airtable to OpenAI and Supabase for rapid responses.

**Custom Browser Extension**: JavaScript-based chatbot overlay deployed in Airtable UI. Ask natural language questions: "Show inventory under $50" or "What's our revenue this week?" Extension parses Airtable responses and presents conversationally. Self-hosted; no third-party API calls expose data.

## Key Architecture Patterns

### Decentralized Data Model with Intelligent Linking
230+ bases organized by function, not by location or time period. Each base uses consistent naming conventions and field structures, enabling n8n to treat them as a unified system. Airtable's record linking feature connects Sales Invoices → Customer → Location → Warehouse, maintaining data integrity across relationships.

### Multi-Location Support with Unified Reporting
Locations maintain independent operational bases (Inventory-Sahara, Inventory-Sunrise, Finance-Sahara, Finance-Sunrise) for autonomy. Master reporting bases aggregate data via Airtable's lookup/rollup fields, enabling location comparison dashboards. Archive bases snapshot location-specific data monthly for historical comparison and migration scenarios.

### Automation-First with Human Oversight
426+ n8n Airtable nodes handle routine tasks (order processing, inventory updates, email notifications). Critical decisions (pricing changes, refunds, hiring) remain human-in-the-loop. n8n workflows flag anomalies for human review; escalation rules ensure urgent items reach the right people within SLAs.

### Backup Strategy for Disaster Recovery
Daily snapshots of critical bases to Supabase PostgreSQL enable rapid point-in-time recovery. Version history on 20+ key bases preserves complete edit trails. Temporal backups dating to 2021 support historical analysis and regulatory audits. Typical recovery time: <2 hours for any base or record.

## Results & Impact

**Operational:**
- Inventory visibility across 2 locations reduced order fulfillment time by ~60% (from manual search to instant lookup)
- Automated returns processing eliminated manual spreadsheet tracking; returns now processed 95%+ within 24 hours
- Marketplace sync reduced duplicate listings by 95%+ through centralized inventory management
- Employee hours tracking automated; eliminates manual timesheet consolidation

**Financial:**
- Multi-location finance system caught $40k+ in reconciliation discrepancies in first year (cross-location pricing errors, duplicate invoices)
- Automated invoice generation reduced billing errors to <1% (was 5–8% with manual entry)
- Real-time profit reporting enables data-driven pricing decisions (vs. delayed month-end analysis)
- Stripe integration auto-reconciles refunds; eliminates manual ledger corrections

**Strategic:**
- AI agents democratize data access: employees ask questions instead of requesting reports (saves ~5 hours/week manager time)
- 4+ years of historical data enables forecasting, trend analysis, and strategic planning
- 50+ active bases support rapid process innovation without system redesign
- Omnichannel architecture enables 5+ marketplace presence without operational overhead

**Technical:**
- 230+ base ecosystem maintained by one person with zero data loss in 4+ years
- 426+ n8n nodes run reliably with 99.5% success rate; failures logged and reviewed daily
- Backup strategy enables disaster recovery (typically <2 hours to restore any base)
- Scales to 100,000+ records per base without performance degradation; Airtable API stays well below rate limits

## How This Was Built

Incrementally over 4+ years, starting with a single Inventory base and expanding as business needs grew. Each new operational layer (Finance, Sales, HR, Marketplace) was designed to integrate seamlessly through:

1. **Standardized Architecture**: Consistent naming conventions (e.g., all tables have Created/Updated timestamps; all linking fields follow pattern {table_name}_id)
2. **Webhook-Driven Sync**: n8n acts as the nervous system, orchestrating data flow between bases and external systems
3. **Historical Preservation**: Archive bases prevent data loss while keeping active bases fast; enables temporal analysis
4. **Human-in-the-Loop Design**: Automation handles 99% of routine tasks; critical decisions stay with people
5. **Modularity**: Each base can be independently backed up, archived, or migrated without affecting others

The result: a system that feels custom-built but uses standard Airtable components—making it maintainable, scalable, and understandable to future team members or consultants.

## Key Design Decisions

**Why 230+ bases instead of 1–2 mega-bases?**
- Performance: Each base stays <50MB; Airtable queries return in <1 second
- Simplicity: Functional bases are easier to understand than a single 10,000-field base
- Resilience: If one base corrupts, others continue operating
- Growth: Adding new modules (e.g., new marketplace) requires new base, not re-architecting core system

**Why Airtable + n8n instead of custom code?**
- Rapid iteration: Changes to base schema or workflow logic don't require code deployment
- Non-technical users: Business stakeholders can modify bases, create views, and add fields without dev help
- Built-in UI: Airtable provides data entry forms, galleries, calendars—no need to build them
- n8n visual workflows: Less error-prone than custom code; easier to debug

**Why 20+ backups per critical base?**
- Audit compliance: Financial bases require version history for regulatory purposes
- Human error recovery: If someone deletes records, restores in minutes instead of re-entering
- Multi-location support: Snapshots enable location-specific archives and what-if scenarios
- Historical analysis: Price trends, customer lifetime value, profitability by category—all enabled by historical data

## Setup & Deployment

This is a **case study and portfolio project**, not a downloadable starter kit. The system is fully deployed and running production auctions across 2+ locations.

**For consultation or integration questions**: Reach out directly. This architecture can be adapted to:
- Multi-location retail or service businesses
- Consignment or marketplace operations
- Subscription-based inventory management
- Complex B2B sales pipelines

**Key takeaway**: Airtable + n8n + smart architecture can replace hundreds of thousands of dollars in custom software while remaining maintainable and understandable.

## What Makes This Interesting

If you're an Airtable user facing any of these challenges:
- Managing inventory across multiple locations or sales channels
- Scaling operations without hiring more admin staff
- Integrating Airtable with external platforms (marketplaces, payment processors, CRM)
- Building AI-powered workflows that query your database in real-time
- Maintaining data integrity and historical audit trails across complex business processes

This system demonstrates solutions to all of them. It's a living proof that with thoughtful design, Airtable can power enterprise-grade operations.

## License

MIT

---

Built by [Ron](https://github.com/702ron) — Portfolio: [github.com/702ron](https://github.com/702ron) | Full-stack business systems architect specializing in Airtable, n8n, and omnichannel operations platforms.
