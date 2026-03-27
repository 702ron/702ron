[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![Airtable](https://img.shields.io/badge/Airtable-Database-blue)](https://airtable.com)
[![Selenium](https://img.shields.io/badge/Selenium-Browser%20Automation-brightgreen)](https://www.selenium.dev)

# Automated 5,000 Monthly Auctions — HiBid Platform

I engineered an enterprise automation platform handling the complete auction lifecycle across two locations. From batch listing creation to real-time bidding and automated returns processing—5,000 monthly auctions run on autopilot with 99.2% uptime. Nine n8n workflows, four custom Python scripts, and 230+ interconnected Airtable bases process 60+ hours of manual work monthly.

## What I Built

- **Hibid Lister (42 nodes)** — Batch creates 100+ auction listings daily with 250+ image processing, dynamic pricing, and category auto-mapping
- **HiBid Watcher (25 nodes)** — Polls active auctions every 5 minutes, captures bid activity from 500+ unique bidders monthly, streams to Airtable in real-time
- **Automated Bidding Stack** — Four implementations: Tkinter GUI for manual oversight, Browserless cloud scaling, cash payment marking, TypeScript production watcher
- **Return & Void Processing (21 nodes)** — Validates refund eligibility, generates Stripe refunds, prevents duplicates via Supabase audit logs; achieves 95%+ same-day rate
- **Buyer Nurture Pipeline** — Segments 300+ high-value buyers monthly through Mailchimp campaigns; syncs bidder enrichment data across platforms

## Architecture

```
HiBid Platform
       │
   ┌───┴───┬──────────┬──────────┐
   │       │          │          │
Hibid   HiBid      Get Bid    Airtable Bases
Lister  Watcher    Users      (230 bases)
(42)    (25)       (16)           │
   │       │          │           │
   └───────┴──────────┴───────────┘
           │
    ┌──────┴──────────┐
    │                 │
Automated Bidding   Return & Void
    (7 nodes)       Processing
                    (21 nodes)
           │
    ┌──────┴────────────┐
    │                   │
Stripe API         Mailchimp
(Refunds)          (Buyer Segments)
```

## Results

- **4,000–5,000 auctions** processed monthly (vs. 10–15 hours/day manual)
- **60+ hours saved** monthly across all workflows
- **500+ unique bidders** tracked and segmented
- **300+ monthly campaigns** sent to high-value buyers
- **95%+ same-day return processing** via automated Stripe refunds
- **85% data entry error reduction** through validation and deduplication
- **99.2% uptime** over 12 months across 9 active workflows
- **250+ images** processed per auction batch automatically

## Tech Stack

n8n, Airtable (230+ bases), Selenium + Playwright, Browserless.io, Python 3.8+, TypeScript, Tkinter, Stripe API, Mailchimp, RabbitMQ, Supabase, Linux/Docker

<!-- Screenshots: [HiBid listings overview, Real-time auction watcher dashboard, Airtable inventory base, Mailchimp campaign results] -->

---

Built by [Ron](https://github.com/702ron)
