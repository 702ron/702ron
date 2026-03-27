# Refund Returns Processing System

![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![Stripe](https://img.shields.io/badge/Stripe-5469D4?style=flat&logo=stripe&logoColor=white) ![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat&logo=rabbitmq&logoColor=white) ![Airtable](https://img.shields.io/badge/Airtable-F7D563?style=flat&logo=airtable&logoColor=black)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/refund-returns-processing)**

End-to-end returns automation that transforms unstructured refund requests into processed refunds. Airtable triggers → RabbitMQ queue → n8n orchestration → Browserless automation → Stripe refunds → immutable audit trail. Handles 6 return categories, multi-location inventory, and idempotent processing.

## What I Built

- **Airtable Form Trigger** - Return requests auto-captured from form submissions without manual data entry
- **RabbitMQ Queuing** - Reliable message queue ensures requests don't drop; enables retry and replay
- **7-Step Automation** - Validation → Void (via Browserless) → Inventory → Refund → Notify → Audit → Complete
- **Browserless Integration** - Headless Chrome automation voids items on auction platform programmatically
- **Stripe Refund Processing** - Automatic refund issuance with transaction tracking and dispute handling
- **6 Return Categories** - Warehouse returns, customer refunds, damaged goods + 3 custom categories with different logic
- **Idempotent Design** - Safely reruns failed workflows without duplicate Stripe refunds
- **Multi-Location Support** - Routes returns to correct warehouse, adjusts regional inventory
- **Immutable Audit Trail** - PostgreSQL logs every step with timestamps, user, status, and error details

## Architecture

```
Airtable Form Submission
        ↓
  RabbitMQ Queue
        ↓
  n8n Workflow Engine
        ↓
    ┌───┴───┬──────────┬──────────┬──────────┬────────┐
    ↓       ↓          ↓          ↓          ↓        ↓
Validate Browserless Inventory  Stripe   Email   PostgreSQL
         (Void)   Update      Refund   Notify    (Audit)
```

**Process Flow:**
1. Customer/staff submits return form in Airtable
2. Webhook adds request to RabbitMQ queue
3. n8n polls queue for new requests
4. Validates return data (SKU, reason, amount)
5. Uses Browserless to void listing on auction platform
6. Updates warehouse inventory in Airtable
7. Issues refund via Stripe API (with idempotency key)
8. Sends customer email notification
9. Logs complete transaction to PostgreSQL audit table
10. Marks request complete; ready for next batch

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Trigger Source** | Airtable Forms | Return request capture from customers/staff |
| **Message Queue** | RabbitMQ | Reliable delivery, retry logic, audit trail |
| **Orchestration** | n8n | Multi-step workflow coordination |
| **Automation** | Browserless (Headless Chrome) | Programmatic void on auction platform |
| **Payments** | Stripe API | Refund issuance and transaction tracking |
| **Inventory** | Airtable / Custom DB | Regional warehouse inventory management |
| **Audit Logs** | PostgreSQL | Immutable transaction history |
| **Notifications** | SendGrid / SMTP | Customer and staff email alerts |

## Key Features

### Multi-Category Returns
Handles warehouse returns, customer refunds, damaged goods, and 3 other categories. Each return type has custom logic for inventory adjustment, refund calculation, and notification templates.

### Idempotent Processing
Safely reruns failed workflows without creating duplicate Stripe refunds. Uses idempotency keys, request deduplication, and state tracking to ensure single-run-once semantics even with retries.

### Multi-Location Support
Routes returns to correct warehouse based on location code. Adjusts regional inventory separately and tracks location-specific return metrics for warehouse optimization.

### Immutable Audit Trail
Every step logged to PostgreSQL with timestamps, user, status, and error details. Enables compliance audits, chargeback disputes, and investigation without relying on scattered email threads.

## Setup

Complete Docker setup, RabbitMQ configuration, n8n workflow exports, Stripe API keys, and troubleshooting guide are available in the [full repository](https://github.com/702ron/refund-returns-processing).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/refund-returns-processing)*
