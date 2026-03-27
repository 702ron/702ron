[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-brightgreen)](https://openai.com)
[![Gmail](https://img.shields.io/badge/Gmail-Email%20API-red)](https://developers.google.com/gmail)
[![MIT License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

# AI Email Labeler Assistant — Intelligent Email Triage System

An intelligent email management system powered by n8n and OpenAI that automatically classifies incoming emails into business categories and applies smart labels to your Gmail inbox in real-time. Pair this with the Gmail Agent V2 for advanced capabilities like thread summarization and intelligent response drafting. Processes 100% of incoming emails without manual classification, enabling teams to focus on high-value business communications instead of email triage.

## What I Built

**Five-workflow email intelligence suite** (18–22 nodes each) handling real-time classification, contextual summarization, and daily reporting:

- **ron@702 Email Labeler (18 nodes)** — Core classification system that triggers on every incoming Gmail message, extracts subject and preview text, sends to OpenAI GPT-4 for intelligent categorization into 6 business categories, applies Gmail labels automatically
- **Gmail Agent V2 (22 nodes)** — Advanced AI agent that reads full email threads (not just headers), generates concise summaries, looks up customer data in Airtable for context, and drafts intelligent replies using business knowledge
- **Daily Email Builder (22 nodes)** — Templated daily email generation that creates formatted newsletters and business updates, dispatches via Gmail
- **702 Auction Morning Report (5 nodes)** — Scheduled 9 AM business intelligence email with key metrics from daily auction operations
- **Email Logging to Google Sheets** — Persistent audit trail and classification history for analytics

## Architecture

```
┌──────────────────────────────────────────────────────────┐
│               Gmail Inbox (Incoming Emails)              │
└────────────────────┬─────────────────────────────────────┘
                     │
                     ▼
        ┌────────────────────────────────────┐
        │ ron@702 Email Labeler              │
        │ (18 nodes, ACTIVE)                 │
        │                                    │
        │ ◆ Gmail trigger (new mail)         │
        │ ◆ Extract headers & preview        │
        │ ◆ Call OpenAI GPT-4                │
        │ ◆ Parse classification result      │
        └────────┬──────────────────────────┘
                 │
        ┌────────▼───────────────┐
        │  OpenAI GPT-4          │
        │  Classification Logic  │
        │  (6-category system)   │
        └────────┬───────────────┘
                 │
    ┌────────────┼────────────┐
    │            │            │
    ▼            ▼            ▼
 Orders      Returns     Inquiries
 Vendors      Spam    High Priority
    │            │            │
    └────────────┼────────────┘
                 │
        ┌────────▼──────────────────────┐
        │  Gmail API                     │
        │  • Add/remove labels           │
        │  • Move to folder              │
        │  • Mark as read/unread         │
        └────────┬──────────────────────┘
                 │
                 ├──────────────────────┐
                 │                      │
                 ▼                      ▼
        ┌──────────────────┐   ┌──────────────────┐
        │ Google Sheets    │   │ Gmail Agent V2   │
        │ Log & Audit      │   │ (22 nodes)       │
        │                  │   │                  │
        │ • Email data     │   │ • Read threads   │
        │ • Categories     │   │ • Summarize      │
        │ • Timestamps     │   │ • Look up cust.  │
        │ • User feedback  │   │ • Draft replies  │
        └──────────────────┘   └──────────────────┘
                 │                      │
                 └──────────┬───────────┘
                            │
                   ┌────────▼──────────┐
                   │  Optional Outputs │
                   │                   │
                   │ • Slack alerts    │
                   │ • Escalations     │
                   │ • CRM updates     │
                   └───────────────────┘
```

**Process Flow:**

1. **Email Trigger** — New email arrives in Gmail inbox; n8n webhook fires via Gmail API push notification
2. **Content Extraction** — Extract from/subject/preview text (no full body reading yet, for speed); timestamp and message ID
3. **AI Classification** — Send extracted fields to OpenAI GPT-4 with a custom prompt defining 6 business categories and classification logic
4. **Category Mapping** — Parse OpenAI response (expects structured JSON with category name and confidence score); map to Gmail label
5. **Label Application** — Gmail API applies corresponding label (e.g., "order-confirmation" label for Orders category); optionally moves to category-specific folder
6. **Logging & Audit** — Record email metadata (from, subject, category, confidence, timestamp) to Google Sheets for analytics and feedback
7. **Optional Advanced Processing** — If high-priority or customer email, trigger Gmail Agent V2 to read full thread, summarize, and draft response

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Automation Engine** | n8n (cloud or self-hosted) | Workflow orchestration, triggers, email API calls |
| **AI/LLM** | OpenAI GPT-4 (gpt-4-turbo) | Email classification, response generation, summarization |
| **Email Service** | Gmail API (via OAuth2) | Read emails, apply labels, move to folders, send replies |
| **Data Store** | Google Sheets API | Email classification log, audit trail, user feedback |
| **Customer Data** | Airtable | Customer lookup, context enrichment for response drafting |
| **Deployment** | n8n Cloud or Docker | Serverless execution or self-hosted on Linux |

## Key Features

### Real-Time Email Classification
The Email Labeler workflow triggers on every incoming email, extracts the subject line and preview text, and sends it to OpenAI GPT-4 with a custom prompt that classifies emails into six business categories:
- **Orders** — Customer purchase requests, order confirmations, bulk inquiries
- **Returns** — Return requests, refund inquiries, item damage claims
- **General Inquiries** — Product questions, pricing requests, general customer service
- **Vendor Communications** — Supplier emails, partnership proposals, delivery notifications
- **Spam/Marketing** — Promotional emails, unsolicited solicitations, newsletters (unless subscribed)
- **High Priority** — Urgent issues, escalations, C-level communications

Gmail labels are applied instantly and automatically, organizing your inbox without manual filing.

### Intelligent Email Agent with Thread Context
Gmail Agent V2 expands on basic classification with advanced capabilities:
- **Full Thread Reading** — Reads entire email conversation history to understand ongoing discussions and context
- **Smart Summarization** — Condenses multi-message threads into actionable 3–5 sentence summaries, highlighting decisions and next steps
- **Customer Lookup** — Queries Airtable for customer history, purchase records, and previous interactions
- **Response Drafting** — Generates contextual replies based on customer data, business rules, and email tone

Perfect for complex customer communications where understanding full conversation history is critical.

### Automated Daily Email Generation
Two production workflows generate intelligence and communications automatically:
- **daily Email Builder** — Creates templated daily emails (newsletter, digest format) with custom content blocks; dispatches via Gmail at scheduled times
- **702 Auction Morning Report** — Generates a business intelligence email at 9 AM daily with key metrics (revenue, item volume, buyer acquisition); provides executive summary for business operations

These workflows demonstrate email generation capabilities and integration with business metrics.

### Multi-Workflow Ecosystem with Flexible Routing
All five workflows operate independently and can be chained together:
- Layer basic classification with advanced agent responses for complex emails
- Combine scheduled reports with real-time classification for comprehensive email operations
- Route emails to different handlers (human, escalation, automation) based on category and priority
- Extend with custom integrations (Slack alerts, CRM updates, ticket creation)

## Workflow Stats

| Workflow | Nodes | Triggers | Status | Purpose |
|----------|-------|----------|--------|---------|
| **ron@702 Email Labeler** | 18 | Gmail Webhook | ACTIVE | Core classification & labeling system |
| **Gmail Agent V2** | 22 | Manual/Webhook | READY | Advanced AI agent with thread context |
| **Gmail Agent** | 16 | Manual/Webhook | ARCHIVED | First-generation email AI agent |
| **daily Email Builder** | 22 | Schedule (daily) | ACTIVE | Templated daily email generation & dispatch |
| **702 Auction Morning Report** | 5 | Schedule (9 AM) | ACTIVE | Daily business intelligence email |

## Classification Examples

### Example 1: Order Confirmation Email
```
From: customer@business.com
Subject: Order #12345 Confirmation - 3 Items

Input to GPT-4:
→ "From: customer@business.com, Subject: Order #12345 Confirmation - 3 Items, Preview: Thank you for your order..."

Output:
→ Category: "Orders" (confidence: 0.98)
→ Gmail Label Applied: "order-confirmation"
```

### Example 2: Return Request Email
```
From: buyer@email.com
Subject: Want to return item from auction #7891

Input to GPT-4:
→ "From: buyer@email.com, Subject: Want to return item from auction #7891, Preview: Item arrived damaged..."

Output:
→ Category: "Returns" (confidence: 0.95)
→ Gmail Label Applied: "return-request"
→ Trigger: Return Void workflow (optional)
```

### Example 3: Vendor Communication
```
From: supplier@vendor.com
Subject: Shipment ETA - Purchase Order 4567

Input to GPT-4:
→ "From: supplier@vendor.com, Subject: Shipment ETA - PO 4567, Preview: Your shipment is scheduled..."

Output:
→ Category: "Vendor Communications" (confidence: 0.92)
→ Gmail Label Applied: "vendor"
```

## How It Works

1. **Email Arrives** in Gmail inbox
2. **Email Labeler Triggers** via Gmail API (on new message)
3. **Extract Content** — Subject, from address, preview text (minimal payload for speed)
4. **OpenAI Classification** — GPT-4 analyzes content and returns category + confidence score
5. **Parse Response** — Extract category name and apply corresponding Gmail label
6. **Log Entry** — Record to Google Sheets for audit trail and analytics
7. **Optional: Gmail Agent V2** — If marked as complex or customer email, read full thread and draft response
8. **High Priority Routing** — If flagged urgent, send Slack alert to ops team or escalate to human handler

## Setup

### Prerequisites
- n8n instance (n8n Cloud or self-hosted)
- Gmail account with API access enabled
- OpenAI API key (GPT-4 access required)
- Google Sheets API enabled (optional, for audit logging)
- Airtable base (optional, for customer lookup in Gmail Agent V2)

### Step-by-Step Installation

1. **Enable Gmail API**
   - Go to Google Cloud Console
   - Create a new project (or use existing)
   - Enable Gmail API and Google Sheets API
   - Create OAuth2 credentials (Web Application type)
   - Download credentials JSON file

2. **Add Gmail Labels in Gmail Settings**
   - In Gmail, create labels for each classification category:
     - order-confirmation
     - return-request
     - inquiry
     - vendor
     - spam-marketing
     - high-priority
   - (Optional) Create corresponding folders/filters for auto-filing

3. **Import Workflows into n8n**
   - Log into n8n dashboard
   - Click Workflows → Import
   - Upload the 5 workflow JSON files in order: Email Labeler, Gmail Agent V2, daily Email Builder, Morning Report, optional logging flow

4. **Configure Credentials in n8n**
   - **Gmail OAuth2**: Add Google OAuth2 credential with email scopes (modify, send, labels)
   - **OpenAI**: Add OpenAI API key (ensure gpt-4-turbo model is accessible)
   - **Google Sheets** (optional): Add Google Sheets credential for audit logging
   - **Airtable** (optional): Add Airtable base and personal access token for customer lookup

5. **Customize Classification Categories**
   - Open Email Labeler workflow
   - Find the "OpenAI Classification" node
   - Edit the prompt to match your business categories (modify the 6 categories as needed)
   - Example customization for legal firm: "Contract Review", "Invoice", "Dispute", "Inquiry", "Spam"

6. **Test End-to-End**
   - Send a test email to your Gmail from another account with subject "Test Order #12345"
   - Monitor n8n execution log (should complete in 5–10 seconds)
   - Verify the corresponding label appears on email in Gmail within 1–2 seconds
   - Check Google Sheets for audit log entry with classification result

7. **Activate for Production**
   - Enable Email Labeler workflow (toggle ON)
   - Configure daily Email Builder cron expression (e.g., `0 9 * * *` for 9 AM daily)
   - Configure Morning Report schedule (e.g., `0 9 * * 1-5` for weekdays only)
   - Set up error notifications to Slack or email
   - Monitor execution daily for the first week; adjust classification prompt if needed

### Example GPT-4 Classification Prompt

```
You are an email classifier for a business email system. Analyze the email below and classify it into ONE of these categories:

1. Orders - Customer purchase requests, order confirmations, bulk inquiries
2. Returns - Return requests, refund inquiries, item damage claims
3. Inquiries - Product questions, pricing requests, general customer service
4. Vendors - Supplier emails, partnership proposals, delivery notifications
5. Spam - Promotional emails, unsolicited solicitations, newsletters
6. HighPriority - Urgent issues, escalations, legal matters

Email:
From: {from_address}
Subject: {subject}
Preview: {preview_text}

Respond in JSON format:
{
  "category": "Orders",
  "confidence": 0.95,
  "reasoning": "Email contains order confirmation language and item count."
}
```

## Customization

- **Classification Categories** — Edit the OpenAI prompt in the Email Labeler to adjust business categories (default: 6 categories)
- **Response Templates** — Modify Gmail Agent V2 response logic for your brand voice and signature
- **Scheduling** — Adjust cron expressions in daily Email Builder and Morning Report workflows
- **Routing Rules** — Add conditional logic to route emails to different handlers by category (e.g., returns → escalate to ops team)
- **Data Enrichment** — Extend Airtable lookup in Gmail Agent V2 to pull additional customer context (purchase history, subscription tier, etc.)
- **Slack Integration** — Add Slack webhook to Email Labeler for real-time high-priority email alerts

## Security Notes

- **API Keys**: Store OpenAI and Google credentials in n8n's encrypted credential vault; never commit to code
- **Gmail OAuth2**: Use minimal scopes (gmail.modify for labels only, not full inbox access); re-authenticate annually
- **Email Content**: Classification runs only on subject/preview, not full email body; full thread reading only in Gmail Agent V2 (manual trigger)
- **PII Handling**: Email addresses and customer data logged to Google Sheets; implement retention policies (delete rows older than 90 days)
- **Rate Limiting**: OpenAI API calls rate-limited to 100 req/min by default; Gmail API allows 500K daily quota; monitor usage in n8n dashboard
- **Error Handling**: Failed classifications (timeout, API errors) default to "Inbox" with no label; manual review required

## License

MIT

---

Built by [Ron](https://github.com/702ron) — Full-stack automation engineer specializing in AI-powered workflows and intelligent business process automation.
