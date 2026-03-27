[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-brightgreen)](https://openai.com)
[![Gmail](https://img.shields.io/badge/Gmail-Email%20API-red)](https://developers.google.com/gmail)

# 100% Automated Email Classification with AI

I built an intelligent email management system powered by n8n and OpenAI that automatically classifies incoming emails into business categories and applies smart labels to Gmail in real-time. Processes every incoming email without manual triage, enabling teams to focus on high-value communications instead of email organization.

## What I Built

- **ron@702 Email Labeler** — 18-node core system triggering on every incoming email, classifying into 6 business categories via GPT-4, applying Gmail labels automatically
- **Gmail Agent V2** — 22-node advanced workflow reading full email threads, generating summaries, looking up customer data in Airtable for intelligent response drafting
- **Daily Email Builder** — 22-node templated email generation creating formatted newsletters and business updates dispatched automatically
- **702 Auction Morning Report** — 5-node scheduled workflow generating 9 AM business intelligence email with key daily metrics
- **Email Logging to Google Sheets** — Persistent audit trail and classification history for analytics

## Architecture

```
Gmail Inbox (Incoming Emails)
       ↓
[Email Labeler] 18 nodes → Extract & classify
       ↓
OpenAI GPT-4 Classification (6 categories)
├─ Orders | Returns | Inquiries
├─ Vendors | Spam | High Priority
       ↓
Gmail API → Apply labels automatically
       ↓
[Gmail Agent V2] → Optional advanced processing
├─ Full thread reading
├─ Summarization
├─ Customer lookup
└─ Response drafting
       ↓
Google Sheets (audit log)
Gmail (labeled inbox)
```

## Results

- **100% incoming email coverage** — Every message classified without manual intervention
- **6 business categories** — Orders, Returns, Inquiries, Vendors, Spam, High Priority
- **Sub-10 second classification** — Real-time labeling on email arrival
- **Intelligent thread context** — Gmail Agent V2 reads full conversations for advanced workflows
- **Zero inbox clutter** — Automatic label organization keeps inbox scannable
- **Extensible routing** — Emails routed to different handlers by category (human, escalation, automation)

## Tech Stack

n8n, OpenAI GPT-4, Gmail API (OAuth2), Google Sheets API, Airtable, JavaScript, n8n workflows (YAML-like config)

<!-- Screenshots: Gmail inbox with auto-applied category labels, Email Labeler workflow in n8n, classification confidence scores -->

---

Built by [Ron](https://github.com/702ron) — Full-stack automation engineer specializing in AI-powered workflows
