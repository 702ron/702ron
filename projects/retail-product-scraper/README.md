[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://python.org)
[![Selenium](https://img.shields.io/badge/Selenium-Browser%20Automation-brightgreen)](https://www.selenium.dev)
[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)

# Real-Time Price Intelligence Across 7 Retailers

I built a comprehensive web scraping toolkit that extracts product data and pricing from major retailers (Macy's, Lowe's, Kohl's, Amazon, liquidation platforms) enabling data-driven bidding and resale margin optimization. Processes 206+ products per run, 53+ manifest files, and enables cross-retailer price comparison for inventory evaluation.

## What I Built

- **Full Macy's Scraper** — Batch scraper handling 206+ products: extracts pricing, SKUs, images, availability with pagination
- **Lowe's API Integration** — Real-time price lookups with barcode/UPC validation for home improvement products
- **Kohl's Manifest Parser** — Automated downloader and parser for 13+ manifest files (53 total) with product-level extraction
- **Amazon ASIN Lookup** — Cross-platform price tracking and inventory matching via Amazon Product API
- **Liquidation Platform Scraper** — Manifest acquisition from Direct Liquidation, liquidation.com with margin calculation
- **Google Trends Integration** — Demand signal extraction; identify emerging product categories and seasonal trends

## Architecture

```
Retail Retailers (Macy's, Lowe's, Kohl's, Amazon, Liquidation)
       ↓
Scraper Layer (Selenium, BeautifulSoup, APIs)
       ↓
Data Processing & Enrichment
├─ Price normalization
├─ SKU/barcode deduplication
├─ Margin calculation
└─ Cross-retailer comparison
       ↓
Output Layer (Airtable, SQLite, JSON/CSV)
       ↓
n8n Workflows → Automated integration
```

## Results

- **206+ products per Macy's run** — Batch scraping with images and pricing
- **7 retailers integrated** — Real-time to batch data sources
- **53 manifest files processed** — Kohl's liquidation with 1,000+ SKUs
- **80%+ cost reduction** — Eliminated manual price lookups and research
- **5-15% margin improvement** — Data-driven pricing intelligence
- **10+ scheduled jobs** — Daily Macy's, hourly Lowe's, manifest checks

## Tech Stack

Python 3.8+, Selenium, Playwright, BeautifulSoup 4, SQLite, Airtable API, n8n, Pandas

<!-- Screenshots: Pricing comparison dashboard, manifest parser results with margin calculations -->

---

Built by [Ron](https://github.com/702ron)
