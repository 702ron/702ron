# Refund Returns Processing System

> **[View full repository with screenshots and code →](https://github.com/702ron/refund-returns-processing)**

End-to-end returns automation that transforms unstructured refund requests into processed refunds. Airtable triggers → RabbitMQ queue → n8n orchestration → Browserless automation → Stripe refunds → immutable audit trail. Handles 6 return categories, multi-location inventory, and idempotent processing.

## Problem
Returns processing is fragmented across multiple systems—customers submit requests via email, support logs them in spreadsheets, finance manually processes refunds, and warehouse staff update inventory. This manual coordination causes delays, duplicate refunds, and audit gaps.

## Solution
Built an automated workflow triggered by Airtable form submissions. Each return request enters a RabbitMQ queue for reliable processing. n8n workflows orchestrate the 7-step process: validation → void on auction platform via Browserless (headless Chrome) → inventory adjustment → Stripe refund issuance → email notification → audit log. Supports 6 return categories with category-specific logic, manages multiple warehouse locations, and uses idempotent processing to prevent duplicate refunds.

## Architecture

```
Airtable Form
    ↓
RabbitMQ Queue
    ↓
  n8n Workflow
    ↓
    ├→ Browserless (Void)
    ├→ Inventory Update
    ├→ Stripe Refund
    ├→ Email Notify
    └→ Audit Log (PostgreSQL)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Trigger | Airtable Forms |
| Queue | RabbitMQ |
| Orchestration | n8n |
| Automation | Browserless (Headless Chrome) |
| Payment | Stripe API |
| Inventory | Airtable / Custom DB |
| Audit Log | PostgreSQL |
| Notifications | SendGrid / SMTP |

## Key Features

### Multi-Category Returns
Handles warehouse returns, customer refunds, damaged goods, and 3 other categories. Each category has custom logic for inventory adjustment and refund calculation.

### Idempotent Processing
Safely reruns failed workflows without creating duplicate Stripe refunds. Request deduplication and state tracking ensure single-run-once semantics.

### Multi-Location Support
Routes returns to correct warehouse, adjusts regional inventory, and tracks location-specific metrics for warehouse optimization.

### Immutable Audit Trail
Every step logged to PostgreSQL with timestamps, user, status, and error details. Enables compliance audits and dispute resolution without relying on email trails.

## Results

- **7-Step Automation**: Complete workflow from request to reconciliation
- **4 Screenshots**: Process diagrams and real-world workflow examples
- **8.5/10 Rating**: Production-grade reliability and completeness
- **6 Return Categories**: Flexible logic handles diverse return reasons
- **Idempotent Design**: Safe for retry without financial risk

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/refund-returns-processing)*
