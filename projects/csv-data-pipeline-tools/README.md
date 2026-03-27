# CSV & Data Pipeline Tools

ETL for Auction and Retail Operations — Transform raw retail manifests into marketplace-ready data at scale.

## Problem

Retail operations generate data in disparate formats (XLS manifests, CSVs, JSON exports) that must be normalized, validated, and uploaded to multiple platforms (Google Sheets, marketplaces, inventory systems). Manual processing is error-prone and doesn't scale. The pipeline must handle lot number reconciliation, multi-stage transformations, and image asset organization.

## Solution

Built an integrated ETL pipeline that transforms raw retail data through multiple stages:

1. **Manifest Parsing** (macys_to_marketplace.py, 46KB): Converts Macy's BOL XLS manifests to marketplace format
2. **Inventory Grouping** (parse csv to pallets): Groups 81KB+ CSVs by warehouse platform (WP2, WP3, WP4)
3. **Image Organization** (Formatter_all_images_first): Prioritizes image assets in auction listings
4. **Barcode Label Generation** (zpl_converter): PNG to ZPL for Zebra printer output
5. **Data Upload**: Automated Google Sheets integration with lot reconciliation
6. **Workflow Automation**: n8n workflows for repeatable transformation steps

```
┌──────────────────────────────────────────────────────────┐
│              CSV Data Transformation Pipeline             │
├──────────────────────────────────────────────────────────┤
│                                                            │
│   Raw Data Sources                                        │
│   ├─ Macy's BOL (XLS)                                    │
│   ├─ Inventory CSV (81KB+)                               │
│   ├─ Auction Exports (JSON)                              │
│   └─ Image Manifests                                     │
│        │                                                  │
│        ▼                                                  │
│   ┌────────────────────────┐                             │
│   │   Manifest Formatter   │  (macys_to_marketplace)    │
│   │   - XLS Parsing        │                             │
│   │   - Column Mapping     │                             │
│   │   - Lot Reconciliation │                             │
│   └────────────────────────┘                             │
│        │                                                  │
│        ▼                                                  │
│   ┌────────────────────────┐                             │
│   │  Inventory Grouping    │  (parse csv to pallets)    │
│   │  - Warehouse Platform  │                             │
│   │  - Pallet Assignment   │                             │
│   │  - Validation          │                             │
│   └────────────────────────┘                             │
│        │                                                  │
│        ▼                                                  │
│   ┌────────────────────────┐                             │
│   │   Image Formatter      │  (Formatter_all_images)    │
│   │   - Asset Prioritized  │                             │
│   │   - Metadata Attached  │                             │
│   └────────────────────────┘                             │
│        │                                                  │
│        ▼                                                  │
│   ┌────────────────────────┐                             │
│   │  Barcode Generation    │  (zpl_converter)           │
│   │  - PNG to ZPL          │                             │
│   │  - Zebra Printer Ready │                             │
│   └────────────────────────┘                             │
│        │                                                  │
│        ▼                                                  │
│   ┌────────────────────────┐                             │
│   │  Upload & Publish      │                             │
│   │  - Google Sheets API   │                             │
│   │  - Marketplace Upload  │                             │
│   │  - Notification        │                             │
│   └────────────────────────┘                             │
│                                                            │
└──────────────────────────────────────────────────────────┘
```

## Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Languages** | Python, Node.js | ETL scripting & orchestration |
| **Data Processing** | pandas, csv module | DataFrame manipulation & parsing |
| **Cloud** | Google Sheets API | Manifest upload & collaboration |
| **File Formats** | XLS, CSV, JSON, PNG, ZPL | Multi-format support |
| **Automation** | n8n workflows | Repeatable transformation chains |
| **Label Printing** | Zebra ZPL | Barcode label generation |

## Key Features

### Multi-Stage ETL Pipeline
- Raw XLS/CSV ingestion with validation
- Column mapping and data normalization
- Lot number reconciliation across systems
- Multi-warehouse inventory grouping (WP2, WP3, WP4)
- Output to marketplace-ready CSV format

### Large-Scale Processing
- Handles 81KB+ inventory CSVs without memory issues
- Processes 27+ auction manifests in batch
- Lot reconciliation across multiple data sources
- Maintains data integrity through transformations

### Google Sheets Integration
- Automated upload to shared Google Sheets
- Full Lot Lists → Manifests → Updated CSV workflow
- Collaborative feedback loops for validation
- API-driven publishing

### Barcode & Asset Support
- PNG to ZPL conversion for Zebra printers
- Image-prioritized auction formatting
- Asset metadata attachment
- Label generation at scale

## Results & Impact

- **Reduced manifest processing time** from 2 hours to 10 minutes per batch
- **Eliminated manual data entry errors** through automated validation
- **Scaled to 1000+ lot items** per processing cycle
- **Improved data quality** with lot reconciliation checks
- **Integrated marketplace uploads** directly from pipeline
- **Enabled team self-service** via Google Sheets interface

## License

MIT

---

Built by [Ron](https://github.com/702ron)
