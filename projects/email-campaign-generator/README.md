# Email Campaign Generator

> **[View full repository with screenshots and code →](https://github.com/702ron/auction-email-automation)**

Cron-driven email automation that fetches trending inventory items from Airtable, applies selection logic, fills responsive MJML email templates, and delivers via Mailchimp. Features scheduled execution, UTM tracking, dry-run previews, deduplication, and error notifications.

## Problem
Marketing teams manually assemble promotional emails—selecting items, writing copy, building templates, and coordinating delivery. High-volume campaigns (weekly or daily) are time-consuming and error-prone. Testing changes requires rebuilding entire campaigns.

## Solution
Built a scheduled automation system that runs on cron intervals (hourly, daily, weekly). Fetches trending products from Airtable, applies merchandising rules (price range, category filters, popularity thresholds), deduplicates against previous campaigns, fills responsive MJML templates with product data, previews results, and sends via Mailchimp. UTM parameters auto-populate for analytics. Dry-run mode enables testing without sending.

## Architecture

```
Cron Trigger
    ↓
Fetch Airtable Inventory
    ↓
Apply Selection Rules
    ↓
Deduplication Check
    ↓
MJML Template Fill
    ↓
    ├→ Dry-Run Preview
    └→ Mailchimp Delivery
    ↓
    ├→ Success Notification
    └→ Error Handling
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Scheduling | Cron (Linux) or n8n |
| Data Source | Airtable API |
| Selection Logic | Custom rules engine |
| Email Template | MJML |
| Delivery | Mailchimp API |
| Analytics | UTM parameters |
| Notifications | SendGrid / SMTP |

## Key Features

### Intelligent Item Selection
Configurable rules filter inventory by price, category, stock level, and popularity. New items highlighted, sale items prioritized, and seasonal products rotated automatically.

### Responsive Email Templates
MJML templates render perfectly on mobile and desktop. Product images, pricing, and CTAs auto-populate from Airtable data.

### Deduplication Logic
Tracks sent items and prevents the same products from appearing in consecutive campaigns. Maintains email recipient fatigue thresholds and prevents campaign redundancy.

### Analytics Tracking
Auto-generates UTM parameters (source, medium, campaign) for each product link. Enables precise ROI attribution in Google Analytics and Mailchimp reporting.

## Results

- **2 Screenshots**: Campaign output examples and Mailchimp integration
- **10 Sections**: Setup, configuration, troubleshooting, and performance tuning
- **7.5/10 Rating**: Reliable for e-commerce and auction-style platforms
- **Error Notifications**: Slack/email alerts on delivery failures or rule conflicts
- **Dry-Run Testing**: Preview emails before sending to live audience

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/auction-email-automation)*
