[![Django](https://img.shields.io/badge/Django-5.0-092E20)](https://www.djangoproject.com)
[![Python](https://img.shields.io/badge/Python-3.12-3776AB)](https://python.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Production-336791)](https://postgresql.org)
[![Docker](https://img.shields.io/badge/Docker-Deployment-2496ED)](https://docker.com)

# 1,000+ Monthly Auctions with Zero Manual Entry

I built an end-to-end Django 5.0 web application automating the complete auction lifecycle from inventory import through HiBid uploads, bidder management, returns processing, and Airtable synchronization. System processes 50+ listings in parallel via Selenium, auto-formats 15+ manifest source types, and provides real-time dashboard for auction metrics and bidder tracking.

## What I Built

- **Auction Formatter** — Parses CSV/Excel manifests, validates product data, normalizes pricing and descriptions for 15+ source types
- **Upload to HiBid** — Selenium-based automation: logs in, creates listings with images, sets bidding rules, manages scheduling
- **Create Auction** — Generates auction specs with automatic categorization, pricing tier assignment, market positioning
- **Void Unpaid on Bid** — Automated unpaid bid processing, Stripe refund initiation, inventory status updates with reputation scoring
- **Remove Duplicates** — Fuzzy matching deduplication using Levenshtein distance for data quality assurance
- **Real-Time Dashboard** — Django web interface tracking active auctions, live bids, winner determination, refund status

## Architecture

```
Inventory Source (CSV/Excel/Manifest)
       ↓
[Auction Formatter] → Parse & validate
       ↓
[Create Auction] → AI categorization & pricing
       ↓
[Upload to HiBid] 50+ parallel + Selenium
       ↓
Django Web Interface
├─ Dashboard (metrics, live trends)
├─ Auction management
├─ Bidder profiles
└─ Returns processing
       ↓
[Void Unpaid] → Stripe refunds & inventory
       ↓
[Remove Duplicates] → Data quality
       ↓
Airtable Sync → Analytics
```

## Results

- **1,000+ auctions monthly** — 333+ per month automated end-to-end
- **Zero manual data entry** — HiBid uploads fully automated
- **50+ parallel uploads** — Via Selenium Grid without blocking
- **Sub-minute per-listing latency** — With 250+ images
- **99% duplicate detection** — Fuzzy matching with Levenshtein distance
- **Real-time bidder tracking** — Live dashboard with reputation scores

## Tech Stack

Django 5.0.7, Python 3.12, PostgreSQL, Selenium 4, Pandas, Airtable API, Stripe API, Docker, Gunicorn, Nginx

<!-- Screenshots: Django dashboard with auction metrics, HiBid upload status tracker, bidder management interface -->

---

Built by [Ron](https://github.com/702ron)
