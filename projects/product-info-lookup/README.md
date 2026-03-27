# Product Info Lookup API

![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![NocoDB](https://img.shields.io/badge/NocoDB-007AFF?style=flat&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) ![Google%20Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?style=flat&logo=google&logoColor=white)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/product-info-lookup)**

Universal product data API that accepts any identifier—ASIN, UPC, FNSKU, URL, or LOT number—and retrieves structured product information from Amazon, Walmart, Target, and Home Depot. Intelligent fallback handling, AI categorization, and smart caching ensure rapid lookups. **Rated 9/10 for production maturity.**

## What I Built

- **Universal Identifier Detection** - Automatically detects ASIN, UPC, FNSKU, product URLs, or LOT numbers without manual specification
- **7-Retailer API Coverage** - Queries Amazon, Walmart, Target, Home Depot, plus Firecrawl fallback and internal sources
- **Parallel Data Fetching** - Simultaneously queries multiple retailers to pick best coverage and availability
- **NocoDB Smart Caching** - Stores previous lookups with TTL policies; dramatically reduces redundant API calls
- **AI Categorization** - Google Gemini and GPT-4 assign structured product categories autonomously
- **Intelligent Fallback** - Firecrawl provides scraping layer when API access is limited
- **Normalized JSON Response** - Returns consistent schema: title, description, pricing, images, specs, merchant details
- **Sub-2 Second Lookups** - Cached queries return in milliseconds; fresh data in under 2 seconds

## Architecture

```
Product Identifier Input
        ↓
  Auto-Detect Type
  (ASIN/UPC/FNSKU/URL/LOT)
        ↓
    ┌───┴────┬────────┬────────┬──────────┐
    ↓        ↓        ↓        ↓          ↓
  Amazon   Walmart   Target   Home Depot  Firecrawl
    └────┬───────────┬────────┬──────────┘
         ↓           ↓        ↓
   Data Normalization
         ↓
   NocoDB Cache
         ↓
   AI Categorization
   (Gemini/GPT-4)
         ↓
  Structured JSON
```

**Process Flow:**
1. Parse incoming identifier (regex detection)
2. Route to appropriate retailer API(s)
3. Query retailers in parallel
4. Check NocoDB cache before calling APIs
5. Normalize results to unified schema
6. Apply AI categorization
7. Cache result for future lookups
8. Return complete product data

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **API Engine** | n8n or Node.js | Workflow coordination, HTTP requests |
| **Identifier Detection** | Regex + Lookup Tables | Determine source and routing |
| **Retailer APIs** | Amazon, Walmart, Target, Home Depot | Primary product data sources |
| **Fallback Scraping** | Firecrawl | When API access restricted |
| **Caching Layer** | NocoDB | Deduplicate requests, improve latency |
| **AI Categorization** | Google Gemini, OpenAI GPT-4 | Product taxonomy assignment |
| **Database** | PostgreSQL | Audit logs, extended metadata |

## Key Features

### Universal Identifier Support
Accepts ASIN, UPC, FNSKU, product URLs, or LOT numbers. The system automatically detects format and routes to the appropriate data source without requiring user input or specification.

### Multi-Retailer Coverage
Queries Amazon, Walmart, Target, and Home Depot in parallel. Automatically picks the retailer with the best data availability, coverage, and current pricing information.

### Intelligent AI Categorization
AI models analyze product data and assign structured categories automatically. Enables downstream taxonomy work and inventory organization without manual tagging.

### Smart Caching Strategy
NocoDB stores previous lookups with configurable TTL policies. Dramatically reduces API calls for repeated product queries while ensuring fresh data for new searches.

## Setup

Detailed setup instructions, Airtable/NocoDB schema, n8n workflow templates, API endpoint reference, and edge case handling are available in the [full repository](https://github.com/702ron/product-info-lookup).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/product-info-lookup)*
