[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://python.org)
[![Selenium](https://img.shields.io/badge/Selenium-Browser%20Automation-brightgreen)](https://www.selenium.dev)
[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![MIT License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

# Retail Product Scraper Suite — Multi-Retailer Price Intelligence Toolkit

A comprehensive web scraping toolkit for extracting product data, pricing information, and inventory details from major retailers and liquidation platforms. Built to support auction/liquidation business operations requiring real-time competitive pricing analysis and product manifest acquisition at scale. Combines Python-based crawlers, JavaScript automation, and n8n workflows to handle 206+ scraped products, 13+ processed manifests, and real-time price comparison across 4+ major retailers.

## What I Built

**Modular scraping ecosystem** handling multiple data sources with format-specific extraction logic:

- **Full_Macys_Scraper (Selenium)** — Batch Macy's product scraper processing 206+ items per run; downloads product images, extracts pricing, SKUs, availability; handles pagination and dynamic content loading
- **Lowe's API Integration** — Real-time price lookup API for home improvement products; supports barcode/UPC validation and cross-retailer price comparison
- **Kohl's Manifest Parser** — Automated manifest downloader and parser; processes 13+ manifest files (53 total) with product-level detail extraction and pricing data enrichment
- **Amazon Product API** — ASIN lookup and price tracking integration; enables cross-platform price comparison and inventory matching
- **Liquidation Platform Scraper** — Automated manifest acquisition from auction sites (Direct Liquidation, liquidation.com); parses product lists for margin calculations
- **n8n Workflow Integrations** — 4 active workflows orchestrating scrapers: amazon_scrape_demo (7 nodes), google_search_tool (5 nodes), lot_lookup_asin (5 nodes), asin_price_lookup (4 nodes)

## Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│              RETAIL PRODUCT SCRAPER SUITE ARCHITECTURE            │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│                  DATA SOURCES & SCRAPERS                          │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌────────────────────┐  ┌──────────────────┐  ┌──────────────┐ │
│  │ Retail Retailers   │  │ Liquidation      │  │ Search APIs  │ │
│  │  • Macy's (206     │  │ Platforms        │  │ • Google     │ │
│  │    products)       │  │ • Direct Liquid  │  │   Search     │ │
│  │  • Lowe's (real-   │  │ • Auctions.com   │  │ • Google     │ │
│  │    time API)       │  │ • Public.com     │  │   Trends     │ │
│  │  • Kohl's (53      │  │                  │  │              │ │
│  │    manifest files) │  │                  │  │              │ │
│  │  • Amazon (ASIN)   │  │                  │  │              │ │
│  └────────────────────┘  └──────────────────┘  └──────────────┘ │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              │ Python (Selenium, Playwright)
                              │ BeautifulSoup, Requests
                              │ TypeScript/Node.js
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│              DATA PROCESSING & ENRICHMENT LAYER                   │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  • Product field extraction (name, SKU, price, availability)     │
│  • Price normalization (remove currency symbols, tax)            │
│  • Barcode/UPC lookup and validation                             │
│  • Cross-retailer price comparison                               │
│  • Manifest parsing (CSV, Excel, JSON formats)                   │
│  • Product matching (SKU/barcode deduplication)                  │
│  • Margin calculation (retail price vs. cost)                    │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                   Structured data (JSON, CSV)
                   SQLite database, Airtable API
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│           OUTPUT & INTEGRATION LAYER                              │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌─────────────────────┐  ┌────────────────┐  ┌──────────────┐  │
│  │ Airtable Tables     │  │ SQLite DB      │  │ JSON/CSV     │  │
│  │ • Inventory (Main)  │  │ • Product Mgmt │  │ Files        │  │
│  │ • Price Tracking    │  │ • Price History│  │ • Reports    │  │
│  │ • Competitor Data   │  │ • Job Results  │  │ • Manifests  │  │
│  └─────────────────────┘  └────────────────┘  └──────────────┘  │
│                                                                   │
│  n8n Workflows: API orchestration, ETL pipelines, automation    │
│                                                                   │
└──────────────────────────────────────────────────────────────────┘
```

**Process Flow:**

1. **Data Source Selection** — User/scheduler selects target retailer (Macy's, Lowe's, Kohl's, Amazon, liquidation platforms)
2. **Retailer-Specific Scraping** — Format-specific scrapers invoked (Selenium for heavy JavaScript sites, BeautifulSoup for static HTML, direct API calls where available)
3. **Content Extraction** — Product fields extracted: name, price, SKU, barcode, images, availability status, category; pagination or manifest parsing handles bulk data
4. **Data Processing** — Price normalization (remove symbols, handle sales/discounts), barcode validation, deduplication by SKU/barcode
5. **Enrichment** — Cross-reference with barcode APIs for product identification; Amazon ASIN lookup for additional pricing intel
6. **Output Generation** — Structured JSON/CSV export; optional SQLite persistence for historical analysis
7. **Integration** — n8n workflows push processed data to Airtable for inventory management, or trigger downstream analysis/bidding decisions

## Tech Stack

| Component | Technologies | Purpose |
|-----------|--------------|---------|
| **Web Scraping** | Python 3.8+, Selenium, Playwright, BeautifulSoup 4, Requests | Browser automation, HTML parsing, dynamic content loading |
| **Data Storage** | SQLite 3, Airtable API | Persistent storage, product catalog, price history, job tracking |
| **APIs** | Amazon Product API, Google Trends API, Barcode APIs (UPC/EAN) | Product enrichment, market analysis, product identification |
| **Automation** | n8n workflows (4 active), Python schedulers (APScheduler) | Workflow orchestration, scheduled scraping, conditional logic |
| **Data Processing** | Python Pandas, regex, JSON/CSV libraries | Data cleaning, transformation, deduplication |
| **Output Formats** | JSON, CSV, Markdown, SQLite | Integration-ready formats for downstream systems |

## Scraper Comparison & Details

| Retailer/Platform | Data Points Extracted | Scraper Tool | Implementation | Scale | Status |
|---|---|---|---|---|---|
| **Macy's** | Product name, price, category, SKU, images (3–5 per product), brand, reviews, availability | Full_Macys_Scraper (Python, Selenium) | Batch scraper with pagination; handles dynamic page loading | 206+ products per run | ✅ Production |
| **Lowe's** | Product name, price, specs (material, dimensions, color), in-stock status, barcode, competitor pricing | lowes_api (REST API + BeautifulSoup) | Hybrid: API for basic data, scraper for specs; cross-retailer comparison | Real-time lookups | ✅ Production |
| **Kohl's** | Manifest items (CSV), product name, quantity, cost, category, barcode/SKU, packaging | kohls (4 script versions, Selenium/Playwright) | Manifest file download + parsing; handles 13+ manifests (53 files total) | 53 files, 1,000+ SKUs | ✅ Production |
| **Amazon** | Product name, ASIN, price, rating, review count, availability, images, prime eligibility | amazon_scrape_demo (n8n, 7 nodes), amazon_product_api (Python) | Direct API (preferred) + Selenium fallback for non-API data | Real-time API lookups | ✅ Production |
| **Direct Liquidation** | Auction lot ID, product name, quantity, condition, category, price per unit, manifest URL | direct_liquidation (Python, BeautifulSoup) | Manifest parsing + lot detail extraction; margin calculation logic | 100+ lot evaluations/day | ✅ Production |
| **Google Search** | Competitor pricing, product availability, regional pricing variations | google_search_tool (n8n, 5 nodes), custom Python script | Google Custom Search API + Selenium for dynamic results | Ad-hoc searches | ✅ Production |
| **Google Trends** | Search volume trends, interest over time, regional breakdowns, related queries | pytrends (Python library, no auth needed) | Trends API wrapper; enables demand signal analysis | Monthly trend reports | ✅ Production |

## Key Features

### Multi-Retailer Price Intelligence
Extract competitive pricing across major retailers in a single operation. Real-time price lookups for Macy's, Lowe's, Kohl's, and Amazon enable data-driven bidding decisions. Compare prices across 4+ platforms simultaneously to identify undervalued inventory and optimize resale margins. Historical price tracking (SQLite storage) enables trend analysis and margin optimization.

### Liquidation Marketplace Integration
Automated manifest downloading and parsing from liquidation platforms (Direct Liquidation, Auctions.com). Extract structured product data from manifest files and match against retail pricing databases to calculate acquisition margins before bidding. Supports batch manifest processing (13+ manifests, 53 files) for bulk inventory evaluation.

### Barcode & ASIN Lookup with Cross-Platform Matching
Integrated barcode/UPC lookup for product identification and enrichment. Amazon ASIN lookup tools enable cross-platform price comparison and inventory matching. Validate product identity across multiple retailers using standardized identifiers (UPC, EAN, ASIN). Airtable integration enables rapid lookup during auction evaluation.

### Intelligent Data Pipeline with Deduplication
End-to-end automation from scraping to warehouse integration. n8n workflows orchestrate data extraction, processing, validation, and push to Airtable inventory management system. Scheduled jobs ensure continuous price data refresh (daily for Macy's, hourly for Lowe's) and manifest monitoring. Deduplication logic prevents duplicate inventory entries.

### Market Research & Trend Analysis
Google Trends integration enables demand signal extraction; identify emerging product categories and seasonal trends. Search volume data informs bidding strategy and inventory acquisition decisions. Enables data-driven category expansion and markdown predictions.

## Scale & Performance

| Metric | Value | Notes |
|--------|-------|-------|
| **Products Scraped** | 206+ | Macy's batch scraper per run |
| **Manifest Files Processed** | 53 | Kohl's liquidation manifests (13+ download sessions) |
| **Retailers Integrated** | 7 | Macy's, Lowe's, Kohl's, Amazon, Direct Liquidation, Google Search, Google Trends |
| **Price Comparison Latency** | Real-time to 24-hour | API-based (real-time) vs. batch scraping (overnight) |
| **Data Export Formats** | 5+ | JSON, CSV, SQLite, Markdown, Airtable push |
| **Scheduled Jobs** | 10+ | Daily Macy's, hourly Lowe's, manifest checks, trend reports |
| **Cost Reduction** | 80%+ | Eliminated manual price lookups and research time |
| **Margin Improvement** | Data-driven | Price intelligence enables 5–15% better margins on acquired inventory |

## Setup

### Prerequisites
- Python 3.8+ with pip package manager
- Selenium WebDriver (ChromeDriver or FirefoxDriver) or Playwright
- API credentials: Amazon Product API, Airtable API, Google Trends API, Barcode APIs (some free, some paid)
- SQLite 3 (included with Python)
- n8n instance (optional, for workflow automation)

### Installation Steps

1. **Clone Repository & Install Dependencies**
   ```bash
   git clone https://github.com/702ron/retail-product-scraper.git
   cd retail-product-scraper
   pip install -r requirements.txt
   ```

2. **Configure API Credentials**
   ```bash
   # Create .env file with your API keys
   cp .env.example .env

   # Edit .env and add:
   AMAZON_API_KEY=your_api_key
   AIRTABLE_API_KEY=your_token
   AIRTABLE_BASE_ID=your_base_id
   GOOGLE_TRENDS_API_KEY=your_key (if paid)
   ```

3. **Set Up Selenium WebDriver**
   ```bash
   # Download ChromeDriver matching your Chrome version
   # https://chromedriver.chromium.org/

   # Or use Playwright (recommended for reliability)
   pip install playwright
   playwright install chromium
   ```

4. **Test Individual Scrapers**
   ```bash
   # Test Macy's scraper
   python Full_Macys_Scraper/main.py --output json

   # Test Lowe's API
   python lowes_api/scraper.py --search "laptop desk"

   # Test Kohl's manifest downloader
   python kohls/manifest_downloader.py --user your_username --password your_password
   ```

### Usage Examples

**Extract Macy's Pricing:**
```bash
python Full_Macys_Scraper/main.py \
  --category "Electronics" \
  --output json \
  --save airtable  # Optional: push to Airtable directly
```

**Run Lowe's Multi-API Price Comparison:**
```bash
python lowes_api/scraper.py \
  --search "kitchen faucet" \
  --compare-amazon \
  --compare-home-depot \
  --output csv
```

**Download & Process Kohl's Manifests:**
```bash
python kohls/manifest_downloader.py \
  --user your_account \
  --password your_password \
  --extract-pricing \
  --save-to-airtable
```

**Execute n8n Workflow (ASIN Lookup):**
```bash
# Use n8n UI or webhook:
curl -X POST http://localhost:3000/webhook/asin-lookup \
  -H "Content-Type: application/json" \
  -d '{"product_name": "MacBook Pro", "asin": "B09..."}'
```

**Web Crawler (Full Site to Markdown):**
```bash
python full_site_markdown/crawler.py \
  --url "https://example.com/products" \
  --depth 2 \
  --output markdown
```

## Project Structure

```
retail-product-scraper-suite/
├── Full_Macys_Scraper/          # Main Macy's batch scraper (Selenium)
│   ├── main.py
│   ├── config.json
│   └── requirements.txt
├── Macys_scraper/               # Alternative Macy's implementation (13 files)
│   ├── scraper.py
│   ├── utils/
│   └── data/
├── lowes_api/                   # Lowe's API + multi-retailer comparison
│   ├── scraper.py
│   ├── api_client.py
│   └── price_comparison.py
├── kohls/                       # Kohl's manifest downloader (4 versions)
│   ├── manifest_downloader.py
│   ├── parser.py
│   └── config/
├── direct_liquidation/          # Direct Liquidation marketplace scraper
│   ├── lot_scraper.py
│   ├── margin_calculator.py
│   └── manifest_parser.py
├── amazon_product_api/          # Amazon ASIN lookup
│   ├── api_client.py
│   └── price_tracker.py
├── jobspy/                      # Job listing scraper + AI scoring (SQLite)
│   ├── scraper.py
│   └── scorer.py
├── crawl4ai/                    # Website content crawler (2025)
│   ├── crawler.py
│   └── config.yaml
├── full_site_markdown/          # Website → markdown converter
│   ├── crawler.py
│   └── markdown_exporter.py
├── pytrends/                    # Google Trends data extraction
│   ├── trends_analyzer.py
│   └── report_generator.py
├── n8n_workflows/               # n8n automation workflows
│   ├── amazon_scrape_demo.json  # (7 nodes, ACTIVE)
│   ├── google_search_tool.json  # (5 nodes)
│   ├── lot_lookup_asin.json     # (5 nodes)
│   └── asin_price_lookup.json   # (4 nodes)
├── tests/                       # Unit tests for scrapers
├── requirements.txt
├── .env.example
└── README.md
```

## Use Cases & Benefits

**Liquidation Business Operations**
- Evaluate acquisition value of auction lots before bidding
- Cross-reference manifest products with retail pricing in real-time
- Calculate expected margins and ROI for bulk buys
- Track competitor pricing for resale optimization
- Make data-driven bidding decisions based on margin targets

**E-Commerce Inventory Management**
- Monitor competitor pricing for dynamic pricing strategies
- Identify price drops and arbitrage opportunities
- Track product availability across retailers (in-stock vs. out-of-stock)
- Build historical pricing datasets for analytics and forecasting
- Maintain competitive pricing without manual research

**Market Research & Trend Analysis**
- Extract search volume trends via Google Trends integration
- Identify emerging product categories and demand signals
- Benchmark retail pricing across markets and regions
- Gather competitive intelligence for business strategy
- Validate product category assumptions before inventory acquisition

## Performance Notes

- **Macy's scraper**: 206+ products per run with image downloads (~30–45 min for full batch)
- **Kohl's manifest processing**: 53 files, 1,000+ SKUs parsed (~5–10 min per manifest)
- **Lowe's comparison**: Real-time pricing for individual lookups (~2–3 sec per product)
- **n8n workflows**: Sub-second API response times for ASIN lookups
- **SQLite**: Efficient local caching; scales to 100,000+ records without performance degradation
- **Memory usage**: ~500MB for Selenium browser instance; scales linearly with data size

## API Rate Limits & Throttling

- **Amazon Product API**: 100 req/sec (paid tier); 5 req/sec (free tier)
- **Google Search**: 100 queries/day (free CSE), unlimited with API key
- **Airtable API**: 5 req/sec (recommended), up to 30 req/sec burst
- **Macy's**: No official API; Selenium scraper includes 2-second delay between requests to respect rate limits
- **Lowe's**: 100 requests per minute (varies by endpoint)

## Security & Legal Notes

- Respect robots.txt and terms of service for all target retailers
- Implement rate limiting (delays between requests) to avoid IP bans
- Use proxy rotation for large-scale scraping if needed (not included, recommend Bright Data or Apify)
- Store API keys in .env files; never commit to version control
- Web scrapers may violate terms of service; use APIs where available
- Validate scraped data for accuracy before using in financial decisions
- Implement error logging and monitoring for scraper reliability

## Contributing

This is a personal portfolio project demonstrating scraping and data integration capabilities. Modifications and extensions welcome for learning purposes:
- Add new retailer scrapers following existing patterns
- Extend n8n workflows for additional data sources
- Improve barcode matching logic with additional validation
- Add visualization dashboards for price trends

## License

MIT License - Use freely for learning and commercial projects.

---

Built by [Ron](https://github.com/702ron) — Retail automation & liquidation business tools specialist | 2024–2025
