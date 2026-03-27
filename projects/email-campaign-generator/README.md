# Email Campaign Generator

![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![Airtable](https://img.shields.io/badge/Airtable-F7D563?style=flat&logo=airtable&logoColor=black) ![Mailchimp](https://img.shields.io/badge/Mailchimp-FFE01B?style=flat&logo=mailchimp&logoColor=black) ![MJML](https://img.shields.io/badge/MJML-Responsive%20Email-blue)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/auction-email-automation)**

Cron-driven email automation that fetches trending inventory items from Airtable, applies selection logic, fills responsive MJML email templates, and delivers via Mailchimp. Features scheduled execution, UTM tracking, dry-run previews, deduplication, and error notifications.

## What I Built

- **Scheduled Cron Execution** - Runs on custom intervals (hourly, daily, weekly) without manual triggering
- **Airtable Inventory Sync** - Fetches trending products with real-time pricing and stock levels
- **Intelligent Selection Rules** - Configurable filters by price range, category, stock level, and popularity
- **Smart Deduplication** - Prevents same products from appearing in consecutive campaigns; maintains recipient fatigue thresholds
- **Responsive MJML Templates** - Mobile-perfect email design with auto-populated product images, pricing, and CTAs
- **UTM Analytics Tracking** - Auto-generates campaign/source/medium parameters for precise ROI attribution
- **Dry-Run Preview Mode** - Test emails before sending to live audience; no sends on failed rules
- **Error Notifications** - Slack/email alerts on delivery failures or rule conflicts
- **Production Analytics** - Mailchimp integration with open rates, click tracking, and subscriber health monitoring
- **2 Comprehensive Screenshots** - Campaign output examples and Mailchimp integration

## Architecture

```
Cron Trigger (Scheduled)
        ↓
Airtable Inventory Query
        ↓
Apply Selection Rules
(Price/Category/Stock/Popularity)
        ↓
Deduplication Check
        ↓
    ┌───┴───┬──────────┐
    ↓       ↓          ↓
 MJML    Dry-Run   Mailchimp
Template  Preview   Delivery
 Fill               (Send)
```

**Process Flow:**
1. Cron trigger fires at scheduled time
2. Fetch products from Airtable with filters (price, category, stock)
3. Apply merchandising rules (highlight new items, prioritize sales)
4. Check against previous campaign data for deduplication
5. Fill MJML template with product data (images, pricing, links)
6. Generate UTM parameters for each product link
7. Render HTML and run dry-run test (optional)
8. Send via Mailchimp to audience list
9. Log delivery status and metrics
10. Send completion/error notification

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Scheduling** | Cron (Linux) or n8n | Recurring execution on custom intervals |
| **Data Source** | Airtable API | Product inventory, pricing, stock levels |
| **Selection Logic** | Custom Rules Engine | Filter, rank, and prioritize products |
| **Email Template** | MJML | Mobile-responsive design with auto-fill |
| **Email Delivery** | Mailchimp API | Campaign sending and subscriber management |
| **Analytics** | UTM Parameters | Campaign/product-level ROI attribution |
| **Notifications** | SendGrid / SMTP | Delivery status and error alerts |

## Key Features

### Intelligent Item Selection
Configurable rules filter inventory by price range, category, stock level, and popularity score. New items automatically highlighted, sale items prioritized, and seasonal products rotated based on date ranges.

### Responsive Email Templates
MJML templates render perfectly on mobile and desktop without media queries. Product images, pricing, descriptions, and CTAs auto-populate from Airtable data without manual copy-pasting.

### Smart Deduplication Logic
Tracks sent items and prevents the same products from appearing in consecutive campaigns. Maintains recipient fatigue thresholds and prevents campaign redundancy—critical for maintaining list health and open rates.

### Advanced Analytics Tracking
Auto-generates UTM parameters (source, medium, campaign) for each product link. Enables precise ROI attribution in Google Analytics and Mailchimp reporting. Track which campaigns and products drive the most revenue.

## Setup

Complete Cron configuration, Airtable schema, MJML template examples, Mailchimp API setup, rule engine documentation, and performance tuning are available in the [full repository](https://github.com/702ron/auction-email-automation).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/auction-email-automation)*
