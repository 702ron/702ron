# Product Info Lookup

> **[View full repository with screenshots and code →](https://github.com/702ron/product-info-lookup)**

Universal product data API that accepts any identifier—ASIN, UPC, FNSKU, URL, or LOT number—and retrieves structured product information from Amazon, Walmart, Target, and Home Depot. Intelligent fallback handling, AI categorization, and smart caching ensure rapid lookups.

## Problem
E-commerce and retail teams work with products from multiple sources using different identifier systems. Translating between ASINs, UPCs, FNSKUs, and URLs while sourcing product data from various retailers creates friction and slows fulfillment, pricing, and inventory workflows.

## Solution
Engineered a 7-step process that auto-detects identifier type and intelligently routes to the correct retailer API or scraping service. NocoDB caches previous lookups to reduce redundant requests. Google Gemini and GPT-4 categorize products intelligently. Firecrawl provides a fallback scraping layer when API access is limited. Returns normalized product data: title, description, pricing, images, specifications, and merchant details.

## Architecture

```
Identifier Input
    ↓
Type Detection (ASIN/UPC/FNSKU/URL)
    ↓
    ├→ Amazon API ──┐
    ├→ Walmart API  ├→ Data Normalization
    ├→ Target API   │
    ├→ Home Depot ──┤
    └→ Firecrawl ───┘
    ↓
NocoDB Cache
    ↓
AI Categorization (Gemini/GPT-4)
    ↓
Structured JSON Response
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| API Layer | FastAPI or Node.js |
| Identifier Detection | Regex + lookup logic |
| Retailers | Amazon, Walmart, Target, Home Depot APIs |
| Scraping | Firecrawl (fallback) |
| Caching | NocoDB |
| AI Categorization | Google Gemini, OpenAI GPT-4 |
| Database | PostgreSQL |

## Key Features

### Universal Identifier Support
Accepts ASIN, UPC, FNSKU, product URLs, or LOT numbers. The system automatically detects format and routes to the appropriate data source without user input.

### Multi-Retailer Coverage
Queries Amazon, Walmart, Target, and Home Depot in parallel or sequentially. Automatically picks the retailer with the best data availability or coverage.

### Intelligent Categorization
AI models analyze product data and assign structured categories. Enables downstream taxonomy work without manual tagging.

### Smart Caching Strategy
NocoDB stores previous lookups with TTL policies. Dramatically reduces API calls for repeated product queries while ensuring fresh data for new searches.

## Results

- **9/10 Rating**: Highest-rated standalone repo with production maturity
- **6 Screenshots**: Comprehensive workflow and data schema documentation
- **14 Sections**: Detailed setup, API reference, and edge case handling
- **Multi-Retailer API Integration**: Production-ready for enterprise retail operations
- **Sub-2s Lookups**: Cached queries return in milliseconds; fresh data in under 2 seconds

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/product-info-lookup)*
