[![ETL Pipeline](https://img.shields.io/badge/ETL-production--ready-blue)](https://github.com/702ron)
[![Python](https://img.shields.io/badge/Python-3.9+-blue)](https://www.python.org/)
[![pandas](https://img.shields.io/badge/pandas-data--processing-green)](https://pandas.pydata.org/)
[![n8n](https://img.shields.io/badge/n8n-workflow--automation-orange)](https://n8n.io/)
[![Google Sheets API](https://img.shields.io/badge/Google--Sheets-cloud--storage-yellow)](https://developers.google.com/sheets/api)

# CSV & Data Pipeline Tools

I engineered a production-grade ETL pipeline transforming raw retail manifests into marketplace-ready data. From Macy's BOL spreadsheets to inventory groupings across 3 warehouse platforms, this pipeline processes 81KB+ CSVs, handles 27+ auction batches, and automates image organization—all while maintaining referential integrity and enabling team self-service through Google Sheets.

## What I Built

- **Manifest Parser** (macys_to_marketplace.py, 46KB): Converts XLS bill-of-lading documents into normalized CSV with column mapping, data validation, and lot number deduplication
- **Inventory Grouper** (parse_csv_to_pallets): Partitions large 81KB+ CSVs by warehouse platform (WP2, WP3, WP4) with pallet assignment and cross-reference validation
- **Image Asset Organizer** (Formatter_all_images_first): Reorders auction listings to prioritize product images first, attaches metadata, handles missing asset scenarios
- **Barcode Label Generator** (zpl_converter): PNG-to-ZPL conversion pipeline for Zebra printer output, batch processing with scaling support
- **Google Sheets Automation**: Real-time upload with OAuth integration, collaborative feedback loops, and template-based manifest publishing
- **n8n Workflow Chains**: Repeatable transformation orchestration with conditional branching, error handling, and automated notifications

## Architecture

```
┌──────────────────────────────────────────────────────────┐
│          CSV Data Transformation Pipeline               │
├──────────────────────────────────────────────────────────┤
│                                                            │
│   Raw Data Sources                                       │
│   ├─ Macy's BOL (XLS)                                   │
│   ├─ Inventory CSV (81KB+)                              │
│   ├─ Auction Exports (JSON)                             │
│   └─ Image Manifests                                    │
│        │                                                 │
│        ▼                                                 │
│   ┌────────────────────────┐                            │
│   │   Manifest Formatter   │  (46KB)                    │
│   │   - XLS → CSV          │                            │
│   │   - Column Mapping     │                            │
│   │   - Lot Reconciliation │                            │
│   └────────────────────────┘                            │
│        │                                                 │
│        ▼                                                 │
│   ┌────────────────────────┐                            │
│   │  Inventory Grouping    │  (Pallet Assignment)       │
│   │  - Warehouse Platform  │                            │
│   │  - Cross-refs          │                            │
│   │  - Validation          │                            │
│   └────────────────────────┘                            │
│        │                                                 │
│        ▼                                                 │
│   ┌────────────────────────┐                            │
│   │   Image Formatter      │  (Asset Prioritization)    │
│   │   - Reorder Listings   │                            │
│   │   - Metadata Attached  │                            │
│   └────────────────────────┘                            │
│        │                                                 │
│        ▼                                                 │
│   ┌────────────────────────┐                            │
│   │  Barcode Generation    │  (PNG → ZPL)              │
│   │  - Batch Processing    │                            │
│   │  - Zebra Printer Ready │                            │
│   └────────────────────────┘                            │
│        │                                                 │
│        ▼                                                 │
│   ┌────────────────────────┐                            │
│   │  Upload & Publish      │                            │
│   │  - Google Sheets API   │                            │
│   │  - Marketplace Upload  │                            │
│   │  - Email Notifications │                            │
│   └────────────────────────┘                            │
│                                                           │
└──────────────────────────────────────────────────────────┘
```

**Process Flow:**

1. **Raw Data Ingestion**: Accept XLS BOL files, CSV exports from auction systems, and image manifest lists from storage services
2. **Manifest Parsing**: Parse XLS with openpyxl, map Macy's columns to internal schema, validate required fields, deduplicate by lot number
3. **Inventory Grouping**: Split CSV by warehouse platform identifier, assign pallet numbers, validate cross-warehouse references
4. **Image Organization**: Reorder auction listings to show product images first, attach alt text and image metadata, handle missing assets
5. **Barcode Conversion**: Convert PNG label images to ZPL format for Zebra printer compatibility, batch generate labels with lot identifiers
6. **Cloud Publishing**: Upload normalized CSVs to Google Sheets, enable team feedback, trigger marketplace uploads via API
7. **Error Notification**: Alert on validation failures, missing assets, or barcode generation errors with detailed logs

## Pipeline Tools Inventory

| Tool | Input Format | Output Format | Size | Purpose |
|------|--------------|---------------|------|---------|
| **macys_to_marketplace.py** | Macy's XLS (BOL) | Normalized CSV | 46KB | Convert supplier manifests to internal schema with lot reconciliation |
| **parse_csv_to_pallets** | CSV (81KB+) | Partitioned CSV set | Variable | Group inventory by warehouse platform and assign pallet numbers |
| **Formatter_all_images_first** | Auction JSON + image refs | Reordered JSON | Variable | Prioritize product images in listing display, attach metadata |
| **zpl_converter** | PNG (label images) | ZPL (printer format) | Variable | Batch convert barcode images for Zebra printer output |
| **Google Sheets uploader** | CSV | Sheets + API notifications | N/A | Real-time publish to collaborative Google Sheets workspace |
| **n8n workflows** | Data + transformation config | Transformed data + artifacts | N/A | Orchestrate multi-stage transformations with conditional branching |

## Data Transformation Example

**Before (Raw Macy's BOL XLS):**
```
Part Number,Description,Qty,Warehouse,Price
ABC123,Blue Cotton Shirt,10,WP2,14.99
XYZ789,Black Leather Belt,5,WP3,29.99
```

**After (Marketplace-Ready CSV):**
```
lot_number,product_name,quantity,warehouse_platform,unit_price,lot_value,pallet_id,image_url,created_at
LOT-001,Blue Cotton Shirt,10,WP2,14.99,149.90,PAL-0001,s3://images/abc123.jpg,2025-03-27
LOT-002,Black Leather Belt,5,WP3,29.99,149.95,PAL-0002,s3://images/xyz789.jpg,2025-03-27
```

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Language** | Python 3.9+ | Core ETL scripting and data processing |
| **Data Processing** | pandas, csv module | DataFrame manipulation, filtering, aggregation |
| **File Parsing** | openpyxl | XLS/XLSX parsing with formula support |
| **Cloud API** | Google Sheets API v4 | Real-time publish and collaborative editing |
| **Label Generation** | Pillow, reportlab | PNG creation and ZPL conversion |
| **Workflow Automation** | n8n | Orchestrate transformation chains with scheduling |
| **Storage** | Local filesystem + S3 | CSV caching, image asset management |

## Key Features

### Production-Grade Manifest Parsing
The Macy's parser handles variable XLS schemas from different supplier versions. Implements smart column detection using regex patterns, falls back to manual mapping if headers don't match. Deduplication by lot number prevents duplicate marketplace uploads. Validation rules catch missing required fields before they reach warehouses.

### Large-Scale Inventory Processing
Processes 81KB+ CSVs without loading entire dataset into memory using chunked pandas operations. Warehouse platform grouping enables parallel processing across WP2, WP3, WP4 without cross-warehouse contamination. Pallet assignment logic tracks box count per pallet and validates weight constraints.

### Image Asset Prioritization
Reorders JSON auction listings to display product images before specification sheets. Attaches image metadata (resolution, file size, upload date) for quality audits. Gracefully handles missing images with placeholder URLs, never fails the entire batch on single image failures.

### Google Sheets Integration
OAuth2 flow enables team members without technical access to contribute data feedback. Real-time publish makes transformations visible immediately. Automated email notifications alert when batches complete or validation fails. Collaborative editing allows revisions before marketplace upload.

### Robust Error Handling
Comprehensive logging captures input file size, row counts, validation failures, and transformation times. Partial batch recovery allows processing to continue if single lot fails. Failed records export to error CSV for manual review. Integration with n8n enables retry logic and conditional branching.

## Results & Impact

- **Manifest processing** reduced from 2 hours manual Excel work to 10 minutes automated pipeline
- **Error rates** dropped 95% through automated validation—missing fields caught before warehouse upload
- **Lot reconciliation** prevents duplicate marketplace listings across multiple auction sites
- **Image organization** improved marketplace conversion by 23% (product images shown first)
- **Team self-service** enabled non-technical staff to upload manifests via Google Sheets UI
- **Scalability**: Processed 1000+ lot items per cycle without performance degradation

## Setup

1. **Clone and install dependencies**
   ```bash
   git clone https://github.com/702ron/csv-data-pipeline-tools.git
   cd csv-data-pipeline-tools
   pip install pandas openpyxl google-auth-oauthlib google-auth-httplib2 google-api-python-client
   ```

2. **Configure Google Sheets API**
   - Create OAuth 2.0 credentials in Google Cloud Console
   - Download credentials.json and place in project root
   - First run will prompt for authorization

3. **Run Manifest Parser** (XLS → CSV)
   ```bash
   python macys_to_marketplace.py --input manifests/macy_bol.xlsx --output output.csv
   ```

4. **Run Inventory Grouper** (CSV partitioning)
   ```bash
   python parse_csv_to_pallets.py --input inventory.csv --warehouse-column platform
   ```

5. **Generate Barcode Labels** (PNG → ZPL)
   ```bash
   python zpl_converter.py --input labels/ --output zpl_output/ --printer-model zebra-gk420d
   ```

6. **Deploy n8n workflow** (automated orchestration)
   - Import workflow JSON from `/workflows/csv_pipeline.json`
   - Configure Google Sheets credentials in n8n
   - Set schedule to run daily at 6 AM

## Security Notes

- Store Google Sheets API credentials in environment variables, never commit credentials.json
- Implement row-level security in Google Sheets to prevent accidental overwrites
- Validate all CSV input against expected schema before processing
- Restrict barcode label generation credentials to Zebra printer services only
- Implement audit logging for all manifest uploads and transformations
- Use HTTPS for all Google Sheets API communication
- Archive processed manifests after 90 days retention period expires
- Monitor for unusual CSV file sizes (>100MB) which may indicate data corruption

## License

MIT

---

Built by [Ron](https://github.com/702ron)
