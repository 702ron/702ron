# AI Email Labeler Assistant

An intelligent email management system powered by n8n and OpenAI that automatically classifies incoming emails and applies smart labels to your Gmail inbox. This suite of automation workflows demonstrates advanced AI-driven email processing, including real-time classification, contextual summarization, and intelligent routing for business correspondence.

## Problem

Email overload in small business environments leads to missed opportunities and delayed responses. Key business emails—customer orders, returns, vendor communications, and urgent inquiries—get lost among spam and marketing noise. Manual classification is time-consuming and inconsistent, while rule-based filters struggle with nuanced business contexts. Without intelligent organization, critical emails require manual triage before any action can be taken.

## Solution

This portfolio project showcases a comprehensive AI-powered email management system built with n8n and OpenAI GPT-4. The Email Labeler workflow automatically classifies incoming emails into business categories and applies Gmail labels in real-time. Paired with the Gmail Agent V2, which reads full email threads, summarizes conversations, and drafts intelligent responses, this system transforms email from a reactive bottleneck into a proactive business tool. All classification logic is handled by OpenAI GPT-4, while automation orchestration happens in n8n, connected to Gmail API and Google Sheets for persistent data management.

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Gmail Inbox                           │
│                   (Incoming Emails)                          │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
        ┌────────────────────────────────────┐
        │     ron@702 Email Labeler          │
        │      (18 nodes, ACTIVE)            │
        │  - Trigger on new mail             │
        │  - Extract email content           │
        │  - Send to OpenAI GPT-4            │
        └────────┬──────────────────────────┘
                 │
        ┌────────▼───────────┐
        │   OpenAI GPT-4     │
        │  Classification    │
        │  (Business Logic)  │
        └────────┬───────────┘
                 │
     ┌───────────┼───────────┐
     │           │           │
     ▼           ▼           ▼
  Orders    Returns   Inquiries
  Vendors    Spam    High Priority
     │           │           │
     └───────────┼───────────┘
                 │
        ┌────────▼──────────────────┐
        │   Gmail API               │
        │  Apply Smart Labels       │
        │  Route High Priority      │
        └───────────────────────────┘
                 │
        ┌────────▼──────────────────┐
        │  Gmail Agent V2           │
        │  (22 nodes)               │
        │  - Read threads           │
        │  - Summarize              │
        │  - Draft responses        │
        │  - Query Airtable         │
        └───────────────────────────┘
```

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Automation Engine** | n8n | Workflow orchestration & automation |
| **AI/LLM** | OpenAI GPT-4 | Email classification & intelligent responses |
| **Email Service** | Gmail API | Read/write emails & label management |
| **Data Store** | Google Sheets | Email log & classification history |
| **Customer Data** | Airtable | Customer lookup & context for responses |
| **Deployment** | n8n Cloud | Self-hosted or cloud execution |

## Key Features

### 🏷️ Real-Time Email Classification

The Email Labeler workflow triggers on every incoming email, extracts the subject line and preview text, and sends it to OpenAI GPT-4 with a custom prompt that classifies emails into business categories:
- **Orders** — Customer purchase requests and confirmations
- **Returns** — Return requests and refund inquiries
- **General Inquiries** — Product questions and customer service
- **Vendor Communications** — Supplier and partner emails
- **Spam/Marketing** — Promotional content and unsolicited mail
- **High Priority** — Urgent or escalated matters

Gmail labels are applied automatically, organizing your inbox without manual intervention.

### 📧 Intelligent Email Agent (V2)

The Gmail Agent V2 expands on basic classification with advanced capabilities:
- **Thread Context** — Reads full email conversations to understand ongoing discussions
- **Smart Summarization** — Condenses long email threads into actionable summaries
- **Response Drafting** — Generates contextual replies based on customer data and business rules
- **Airtable Integration** — Looks up customer history and details to personalize responses

Perfect for handling complex customer communications where context is critical.

### ⏰ Automated Daily Email Reports

Two production workflows generate intelligence and communications automatically:
- **daily Email Builder** — Creates and dispatches templated daily emails with curated content
- **702 Auction Morning Report** — Generates a business intelligence report at 9 AM with key metrics

These demonstrate email generation capabilities and scheduled automation patterns.

### 🔄 Multi-Workflow Ecosystem

All five workflows operate independently and can be chained together:
- Layer basic classification with advanced agent responses
- Combine with daily reporting for comprehensive email operations
- Flexible routing based on email category and priority

## Results & Impact

- **100% automated email classification** — All incoming emails processed without manual labeling
- **5+ email categories** — Consistent, AI-driven organization system
- **Real-time routing** — High-priority emails surface immediately
- **Reduced manual triage** — Eliminating time spent manually filing emails
- **Scalable pattern** — Workflows operate at high volume without degradation
- **Production-ready** — 3 ACTIVE workflows running continuously in production

## Component Breakdown

| Workflow | Nodes | Status | Purpose |
|----------|-------|--------|---------|
| **ron@702 Email Labeler** | 18 | ACTIVE | Core email classification & labeling system |
| **Gmail Agent V2** | 22 | Ready | Advanced AI agent with thread context & summarization |
| **Gmail Agent** | 16 | Archived | First-generation email AI agent |
| **daily Email Builder** | 22 | ACTIVE | Automated daily email generation & dispatch |
| **702 Auction Morning Report** | 5 | ACTIVE | Daily 9 AM business intelligence email |

## How It Works

1. **Email arrives** in Gmail inbox
2. **Email Labeler workflow triggers** on new mail event
3. **Email content extracted** (subject, sender, preview text)
4. **OpenAI GPT-4 classifies** the email based on business logic prompt
5. **Gmail labels applied** automatically (e.g., "order", "return", "inquiry")
6. **High-priority emails** optionally routed to human handlers or escalation workflows
7. **Optional: Gmail Agent V2** reads full thread and can draft responses using Airtable customer data

## Getting Started

To use these workflows in your own n8n instance:

1. **n8n Setup** — Deploy n8n or use n8n Cloud
2. **Gmail API Connection** — Add Gmail credentials to n8n
3. **OpenAI API Key** — Add your OpenAI GPT-4 API key to n8n credentials
4. **Airtable (Optional)** — Connect Airtable base for customer data (for Gmail Agent V2)
5. **Google Sheets (Optional)** — Connect for email logging & audit trail
6. **Import Workflows** — Download workflow JSONs and import into your n8n instance
7. **Activate** — Enable "ACTIVE" workflows to begin automated classification

Customize the classification categories and OpenAI prompts to match your business domain and email patterns.

## Customization

- **Classification Categories** — Edit the OpenAI prompt in the Email Labeler to adjust business categories
- **Response Templates** — Modify Gmail Agent V2 response logic for your brand voice
- **Scheduling** — Adjust cron expressions in daily Email Builder and Morning Report
- **Routing Rules** — Add conditional logic to route emails to different handlers by category
- **Data Enrichment** — Extend Airtable lookup to pull additional customer context

## License

MIT

---

**Built by [Ron](https://github.com/702ron)** — Full-stack automation engineer specializing in AI-powered workflows and business process optimization.
