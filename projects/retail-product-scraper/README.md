# Retail Product Scraper Suite

A comprehensive web scraping toolkit for extracting product data, pricing information, and inventory details from major retailers and liquidation platforms. Built to support auction/liquidation business operations requiring real-time competitive pricing analysis and product manifest acquisition at scale.

## Problem

E-commerce and liquidation businesses need accurate, up-to-date retail pricing data to determine resale values and margins. Manual price lookups are time-consuming and fail to scale with inventory volume. Extracting structured product data from multiple retailers with different site architectures requires flexible, maintainable scraping solutions.

## Solution

A modular web scraping suite combining Python-based crawlers, JavaScript automation tools, and n8n workflows to extract product data across multiple retailers. The toolkit handles pricing lookups, product comparisons, manifest downloads, and automated data pipeline integration with inventory management systems.

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     RETAIL PRODUCT SCRAPER SUITE                 │
└─────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│                      DATA SOURCES & SCRAPERS                      │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌────────────────┐  ┌─────────────────┐  ┌────────────────────┐ │
│  │    Retailers   │  │  Liquidation    │  │  Search & Trends   │ │
│  │  • Macy's      │  │   Platforms     │  │  • Google Search   │ │
│  │  • Lowe's      │  │ • Direct Liquid │  │  • Google Trends   │ │
│  │  • Kohl's      │  │ • Auctions      │  │                    │ │
│  │  • Amazon      │  │                 │  │                    │ │
│  └────────────────┘  └─────────────────┘  └────────────────────┘ │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              │ Python (Selenium, Playwright)
                              │ BeautifulSoup, Requests
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                   DATA PROCESSING & ENRICHMENT                    │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  • Price extraction & normalization                              │
│  • Barcode/UPC lookup & validation                               │
│  • Cross-retailer price comparison                               │
│  • Manifest parsing & product matching                           │
│  • Data deduplication & quality assurance                        │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              │ Structured data (JSON, CSV)
                              │ SQLite, Airtable API
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                    OUTPUT & INTEGRATION LAYER                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌────────────────────┐  ┌──────────────────┐  ┌──────────────┐ │
│  │  Airtable Tables   │  │  Database (SQL)  │  │  JSON/CSV    │ │
│  │  • Inventory       │  │  • Product Mgmt  │  │  Files       │ │
│  │  • Price Tracking  │  │  • Price History │  │  • Reports   │ │
│  └────────────────────┘  └──────────────────┘  └──────────────┘ │
│                                                                   │
│  n8n Workflows: API orchestration, ETL pipelines, automation    │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Component | Technologies | Purpose |
|-----------|--------------|---------|
| **Web Scraping** | Python, Selenium, Playwright, BeautifulSoup, Requests | Browser automation & HTML parsing |
| **Data Storage** | SQLite, Airtable API | Persistent storage & inventory management |
| **APIs** | Amazon Product API, Google Trends API, Barcode APIs | Product data enrichment |
| **Automation** | n8n, Python scripts | Workflow orchestration & scheduling |
| **Data Processing** | Python (Pandas), regex | Data cleaning & transformation |
| **Output Formats** | JSON, CSV, Markdown | Integration-ready data formats |

## Supported Retailers & Data Extraction

| Retailer/Platform | Data Points | Scraper | Status |
|-------------------|------------|---------|--------|
| **Macy's** | Product name, price, SKU, images, availability | `Full_Macys_Scraper` / `Macys_scraper` | ✅ Production |
| **Lowe's** | Product specs, pricing, inventory, barcode lookups | `lowes_api` | ✅ Production |
| **Kohl's** | Manifest data, product listings, pricing | `kohls` | ✅ Production |
| **Amazon** | Product data, pricing, ASIN, reviews | `amazon_scrape_demo` (n8n) | ✅ Production |
| **Direct Liquidation** | Auction lots, manifests, product details | `direct_liquidation` | ✅ Production |
| **Google Search** | Competitor pricing, product availability | `google_search_tool` (n8n) | ✅ Production |
| **Google Trends** | Search trends, market demand signals | `pytrends` | ✅ Production |

## Key Features

### Multi-Retailer Price Intelligence
Extract competitive pricing across major retailers in a single operation. Compare prices in real-time to determine optimal resale margins and identify undervalued inventory opportunities. Automated price tracking across Macy's, Lowe's, Kohl's, and Amazon with historical data storage for trend analysis.

### Liquidation Marketplace Integration
Automated manifest downloading from liquidation platforms (Direct Liquidation, auction sites). Parse structured product data from manifest files and match against retail pricing databases to calculate acquisition margins and expected ROI before bidding.

### Barcode & ASIN Lookup
Integrated barcode/UPC lookup for product identification and enrichment. Amazon ASIN lookup tools enable cross-platform price comparison and inventory matching. Validate product identity across multiple retailers using standardized identifiers.

### Intelligent Data Pipeline
End-to-end automation from scraping to warehouse integration. n8n workflows orchestrate data extraction, processing, validation, and push to Airtable inventory management system. Scheduled jobs ensure continuous price data refresh and manifest monitoring.

## Results & Impact

- **206+ products** successfully scraped and tracked from Macy's
- **13+ Kohl's manifests** (53 files) processed with pricing data extraction
- **Real-time price comparison** across 4+ major retailers
- **Automated manifests** downloaded and parsed from liquidation platforms
- **Cost reduction**: Eliminated manual price lookups, reducing research time by 80%+
- **Margin optimization**: Price intelligence enables data-driven bidding on liquidation inventory
- **Inventory accuracy**: Barcode validation ensures correct product matching across platforms

## Quick Start

### Prerequisites
- Python 3.8+
- Selenium WebDriver or Playwright
- API credentials (Amazon Product API, Airtable)

### Usage

**Extract Macy's pricing:**
```bash
python Full_Macys_Scraper/main.py
```

**Run Lowe's price comparison:**
```bash
python lowes_api/scraper.py --search "product name"
```

**Download Kohl's manifests:**
```bash
python kohls/manifest_downloader.py
```

**Execute n8n workflow:**
```bash
# Use n8n UI to trigger workflows or webhook endpoints
# Example: amazon_scrape_demo.json (7 nodes, active)
```

**Web crawler (full markdown export):**
```bash
python full_site_markdown/crawler.py --url "https://example.com"
```

## Project Structure

```
retail-product-scraper-suite/
├── Full_Macys_Scraper/          # Comprehensive Macy's scraper (Selenium)
├── Macys_scraper/               # Alternative Macy's implementation (13 files)
├── lowes_api/                   # Lowe's + multi-API price comparison
├── kohls/                        # Kohl's manifest downloader (4 versions)
├── direct_liquidation/          # Liquidation marketplace scraper
├── jobspy/                       # Job listing scraper + AI scoring (SQLite)
├── crawl4ai/                     # Website content crawler (2025)
├── full_site_markdown/          # Website → markdown converter
├── pytrends/                     # Google Trends data extraction
├── n8n_workflows/               # n8n automation workflows
│   ├── amazon_scrape_demo.json   # (7 nodes, ACTIVE)
│   ├── google_search_tool.json   # (5 nodes)
│   ├── lot_lookup_asin.json      # (5 nodes)
│   └── asin_price_lookup.json    # (4 nodes)
└── README.md
```

## Use Cases

**Liquidation Business Operations**
- Evaluate acquisition value of auction lots before bidding
- Cross-reference manifest products with retail pricing
- Calculate expected margins and ROI
- Track competitor pricing for resale optimization

**E-Commerce Inventory Management**
- Monitor competitor pricing for dynamic pricing strategies
- Identify price drops and arbitrage opportunities
- Track product availability across retailers
- Build historical pricing datasets for analytics

**Market Research & Trend Analysis**
- Extract search volume trends via Google Trends integration
- Identify emerging product categories and demand signals
- Benchmark retail pricing across markets
- Gather competitive intelligence for business strategy

## API Integration

- **Airtable API**: Direct inventory table updates with scraped data
- **Amazon Product API**: ASIN lookup and pricing enrichment
- **Google Trends API**: Market demand signal extraction
- **Barcode APIs**: UPC/EAN validation and product identification
- **n8n**: Workflow orchestration, API call chaining, conditional logic

## Performance Notes

- Macy's scraper: 206+ products per run with image downloads
- Kohl's manifest processing: 53 files, automated parsing
- Lowe's comparison: Real-time pricing across multiple lookups
- n8n workflows: Sub-second API response times for ASIN lookups
- Memory efficient: SQLite for local caching, Airtable for long-term storage

## Contributing

This is a personal portfolio project. Modifications welcome for learning purposes. When extending functionality:
- Test scrapers in development before production use
- Respect robots.txt and terms of service
- Implement rate limiting to avoid IP bans
- Log errors and failures for debugging

## License

MIT License - Use freely for learning and commercial projects.

---

**Built by [Ron](https://github.com/702ron)** | Retail automation & liquidation business tools | 2024-2025
