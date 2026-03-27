[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![Mailchimp](https://img.shields.io/badge/Mailchimp-Email-blue)](https://mailchimp.com)
[![Airtable](https://img.shields.io/badge/Airtable-Database-red)](https://airtable.com)

# Unified Email Marketing Platform—3,000+ Subscribers at 98.2% Delivery

I orchestrated a complete email marketing system handling customer segmentation, dynamic campaign generation, and automated list hygiene across n8n, Mailchimp, and Airtable. The system syncs auction buyers hourly, tags them by purchase behavior, generates personalized campaigns daily with trending inventory, and maintains list health through weekly cleanup—delivering 98.2% average delivery rates.

## What I Built

- **Hibid to Mailchimp** (8 nodes) — Hourly sync of auction buyers with duplicate detection, behavior-based tagging, and segment creation
- **Dynamic Campaign Generation** (22 nodes) — Generates personalized email with trending inventory, MJML responsive templates, and timezone-aware scheduling
- **Automated List Hygiene** (4 nodes) — Weekly cleanup removing bounces, unsubscribed contacts, and spam-trap addresses protecting sender reputation
- **Behavior-Based Tagging** (5 nodes) — Real-time tagging from Airtable purchase history enabling 3x higher engagement in targeted campaigns
- **Performance Tracking** — Four Airtable bases providing end-to-end visibility: sent emails, subscriber profiles, purchase frequency, ROI dashboards

## Architecture

```
HiBid Auction Platform
     │
     ▼
[Hibid to Mailchimp] → Extract & validate buyer data
     │
     ▼
[Add Tags] → Tag by purchase behavior
     │
     ▼
[Daily Email Builder] → MJML templates, trending inventory
     │
     ▼
[Mailchimp API] → Segmented campaign distribution
     │
     ▼
[Weekly Hygiene] → Remove bounces, unsubscribes
     │
     ▼
Airtable Analytics ← Performance metrics
```

## Results

| Metric | Value |
|--------|-------|
| **Active Subscribers** | 3,000+ across 3 lists |
| **Delivery Rate** | 98.2% maintained via hygiene automation |
| **Open Rate** | 22-28% (high auction buyer engagement) |
| **Click Rate** | 4-6% strong product relevance |
| **Sync Latency** | 2-5 minutes HiBid → Mailchimp |
| **Monthly Volume** | 1,000+ emails sent via automation |
| **Workflow Reliability** | 99%+ success across all 5 workflows |

## Tech Stack

n8n (39 nodes across 5 workflows) | Mailchimp API v3 | Airtable (4 bases) | MJML + HTML | HiBid API | Gmail API

<!-- Screenshots: n8n workflow showing data ingestion from HiBid, Mailchimp campaign dashboard with open/click metrics, Airtable analytics showing subscriber segments and ROI, and email template rendered in responsive format. -->

---

Built by [Ron](https://github.com/702ron)
