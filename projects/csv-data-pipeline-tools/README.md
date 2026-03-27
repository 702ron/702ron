[![ETL Pipeline](https://img.shields.io/badge/ETL-production--ready-blue)](https://github.com/702ron)
[![Python](https://img.shields.io/badge/Python-3.9+-blue)](https://www.python.org/)
[![pandas](https://img.shields.io/badge/pandas-data--processing-green)](https://pandas.pydata.org/)
[![n8n](https://img.shields.io/badge/n8n-workflow--automation-orange)](https://n8n.io/)
[![Google Sheets API](https://img.shields.io/badge/Google--Sheets-cloud--storage-yellow)](https://developers.google.com/sheets/api)

# Manifest Processing from 2 Hours to 10 Minutes—95% Error Reduction

I engineered a production-grade ETL pipeline transforming raw retail manifests into marketplace-ready data. Processes 81KB+ CSVs, handles 27+ auction batches, handles variable supplier XLS schemas, and automates image organization—all while maintaining referential integrity and enabling team self-service through Google Sheets.

## What I Built

- **Manifest Parser** (46KB) — Converts Macy's XLS bill-of-lading documents into normalized CSV with column mapping, data validation, and deduplication
- **Inventory Grouper** — Partitions large CSVs by warehouse platform (WP2, WP3, WP4) with pallet assignment and cross-reference validation
- **Image Asset Organizer** — Reorders auction listings to prioritize product images first, attaches metadata, handles missing assets gracefully
- **Barcode Label Generator** — PNG-to-ZPL conversion pipeline for Zebra printer output with batch processing and scaling
- **Google Sheets Automation** — Real-time OAuth-enabled upload with collaborative feedback loops and template-based publishing
- **n8n Workflow Chains** — Repeatable transformation orchestration with conditional branching, error handling, and notifications

## Architecture

```
Raw Data Sources
├─ Macy's BOL (XLS)
├─ Inventory CSV (81KB+)
└─ Image Manifests
     │
     ▼
Manifest Formatter (Column mapping, dedup)
     │
     ▼
Inventory Grouping (Pallet assignment, validation)
     │
     ▼
Image Formatter (Asset prioritization)
     │
     ▼
Barcode Generation (PNG → ZPL)
     │
     ▼
Upload & Publish (Google Sheets + Marketplace)
```

## Results

| Metric | Impact |
|--------|--------|
| **Processing time** | 2 hours manual Excel → 10 minutes automated |
| **Error rate** | 95% reduction through automated validation |
| **Marketplace listings** | Duplicate prevention via lot reconciliation |
| **Conversion improvement** | 23% gain from product images shown first |
| **Team enablement** | Non-technical staff upload manifests via Google Sheets |
| **Scale capacity** | 1000+ lot items per cycle without degradation |

## Tech Stack

Python 3.9+ | pandas | openpyxl | Google Sheets API v4 | n8n | Pillow | reportlab | S3 storage

<!-- Screenshots: CSV pipeline processing Macy's manifest into normalized data, image reordering showing product images prioritized, barcode label generation in ZPL format, and Google Sheets upload interface. -->

---

Built by [Ron](https://github.com/702ron)
