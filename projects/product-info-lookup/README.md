![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![NocoDB](https://img.shields.io/badge/NocoDB-007AFF?style=flat&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) ![Google Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?style=flat&logo=google&logoColor=white)

# Universal Product Lookup Across 4 Retailers — Any Identifier, Instant Data

**[Full Repository](https://github.com/702ron/product-info-lookup)**

Universal product data API that accepts any identifier — ASIN, UPC, FNSKU, URL, or LOT number — and retrieves structured information from Amazon, Walmart, Target, and Home Depot. Intelligent fallback handling, AI categorization, and smart caching ensure sub-2-second lookups.

[![Main Workflow](./screenshots/main-workflow.png)](./screenshots/main-workflow.png)

## What I Built

- **Universal Identifier Detection** — Auto-detects ASIN, UPC, FNSKU, product URLs, or LOT numbers without manual specification
- **4-Retailer Parallel Queries** — Amazon, Walmart, Target, Home Depot queried simultaneously for best coverage
- **AI Categorization** — Google Gemini and GPT-4 assign structured product categories autonomously
- **NocoDB Smart Caching** — TTL-based cache eliminates redundant API calls; cached queries return in milliseconds
- **Firecrawl Fallback** — Scraping layer kicks in when API access is limited

## Screenshots

| ASIN Tool Workflow | UPC Tool Workflow |
|:-:|:-:|
| [![ASIN Tool](./screenshots/asin-tool-workflow.png)](./screenshots/asin-tool-workflow.png) | [![UPC Tool](./screenshots/upc-tool-workflow.png)](./screenshots/upc-tool-workflow.png) |

| FNSKU Tool Workflow | URL Tool Workflow |
|:-:|:-:|
| [![FNSKU Tool](./screenshots/fnsku-tool-workflow.png)](./screenshots/fnsku-tool-workflow.png) | [![URL Tool](./screenshots/url-tool-workflow.png)](./screenshots/url-tool-workflow.png) |

| Lot Lookup Workflow | NocoDB Cache Table |
|:-:|:-:|
| [![Lot Lookup](./screenshots/lot-lookup-workflow.png)](./screenshots/lot-lookup-workflow.png) | [![NocoDB Cache](./screenshots/nocodb-cache-table.png)](./screenshots/nocodb-cache-table.png) |

## Architecture

```
Product Identifier Input
        ↓
  Auto-Detect Type (ASIN/UPC/FNSKU/URL/LOT)
        ↓
    ┌───┴────┬────────┬────────┬──────────┐
    ↓        ↓        ↓        ↓          ↓
  Amazon   Walmart   Target   Home Depot  Firecrawl
    └────────┴────────┴────────┴──────────┘
                     ↓
           NocoDB Cache → AI Categorization → Structured JSON
```

## Results

- **Sub-2-second lookups** for fresh data; milliseconds for cached
- **5 identifier types** auto-detected and routed
- **4 major retailers** queried in parallel per request
- **AI categorization** via Gemini + GPT-4 without manual tagging
- **7 workflow screenshots** documenting every tool and integration

## Tech Stack

n8n, NocoDB, OpenAI GPT-4, Google Gemini, Firecrawl, Airtable, PostgreSQL

---

Built by [Ron](https://github.com/702ron)
