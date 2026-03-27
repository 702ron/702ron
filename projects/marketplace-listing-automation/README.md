[![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)](https://n8n.io)
[![Selenium](https://img.shields.io/badge/Selenium-Automation-43B01D)](https://selenium.dev)
[![Playwright](https://img.shields.io/badge/Playwright-CloudBrowser-2EAC6D)](https://playwright.dev)
[![Browserless](https://img.shields.io/badge/Browserless-Headless-FFB81C)](https://browserless.io)

# Automated 40,000+ Annual Auctions Across 5 Platforms

I engineered a multi-platform marketplace automation suite that orchestrates inventory uploads across HiBid, OfferUp, eBay, Amazon, and Liquidation.com. The system processes 250+ images per auction, handles 40,000+ auctions annually, and achieves 20:1 ROI through automated listing creation and intelligent bid management. No manual data entry required.

## What I Built

- **Hibid Lister** — 42-node n8n workflow orchestrating end-to-end HiBid auction creation: image uploads, bidding parameters, scheduling with real-time Airtable status
- **OfferUp Template Creator** — 11-node workflow generating platform-specific listings with image optimization and API integration
- **Manifest Formatter** — Python script converting Macy's liquidation manifests and pallet inventories into platform-specific formats with SKU mapping
- **Image Processing Pipeline** — Handles 250+ images per auction: resize, compress, batch CDN upload with 95%+ first-attempt success
- **Auction Monitoring & Bidding** — Windmill Scraper (TypeScript/Playwright) and Browserless Bid engine track competitor bidding patterns and execute automated bidding

## Architecture

```
Inventory Sources (CSV, Database, Manifests)
       ↓
[Manifest Formatter] → Normalize & validate
       ↓
[Image Processing] → Resize, compress, upload to CDN
       ↓
[Airtable Orchestrator] 7 bases → Trigger platform workflows
       ↓
Platform Workflows
├─ [HiBid Lister] 42 nodes + Selenium
├─ [OfferUp Creator] 11 nodes
├─ [eBay Feed Manager]
└─ [Amazon Vendor Upload]
       ↓
Auction Monitoring & Analytics
├─ [Windmill Scraper] → Track competitor bids
├─ [Browserless Bid] → Automated bidding
└─ Airtable Dashboards → ROI tracking
```

## Results

- **40,000+ auctions annually** — 333+ per month automated end-to-end
- **5 marketplace platforms** — HiBid, OfferUp, eBay, Amazon, Liquidation.com
- **250+ images per auction** — Optimized and uploaded automatically in <5 minutes
- **Sub-minute listing creation** — Per-listing with parallel Selenium processing
- **100% automated bid monitoring** — Cloud-based via Browserless
- **20:1 ROI** — Labor reduction and improved velocity

## Tech Stack

n8n, Python, TypeScript, Selenium 4, Playwright, Browserless.io, PIL/Pillow, Airtable

<!-- Screenshots: Dashboard showing auction metrics and status tracker, HiBid marketplace listing with automated images -->

---

Built by [Ron](https://github.com/702ron)
