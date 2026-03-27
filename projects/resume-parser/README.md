# Resume Parser for Airtable

> **[View full repository with screenshots and code →](https://github.com/702ron/resume-parser-airtable)**

Automated recruitment pipeline that monitors Gmail for resume attachments, extracts and parses them with GPT-4, and populates Airtable and Google Drive. Processes candidate contact info, work history, key highlights, and 5 additional fields for instant organization and searchability.

## Problem
Recruiting teams spend hours manually copying candidate data from resumes into spreadsheets. Email inboxes become resume dumps, key information is mistyped, and sorting qualified candidates requires scanning dozens of PDFs. Dedicated recruitment platforms are expensive and rigid.

## Solution
Built a 6-step pipeline that monitors a Gmail inbox for resume attachments. Files are extracted, sent to GPT-4 for intelligent parsing (contact, work history, highlights, education, skills, certifications, salary expectations, and availability), stored in Google Drive for archival, and key fields are pushed to Airtable for sorting, filtering, and pipeline management. Customizable for LinkedIn, Indeed, or direct application flows.

## Architecture

```
Gmail Monitoring
    ↓
Attachment Extraction
    ↓
GPT-4 Resume Parsing
(8 structured fields)
    ↓
    ├→ Google Drive Storage
    └→ Airtable Base
        ↓
    Searchable Records
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Email | Gmail API |
| Parser | OpenAI GPT-4 |
| Database | Airtable |
| File Storage | Google Drive API |
| Orchestration | n8n or Zapier |
| Backup | PostgreSQL (optional) |

## Key Features

### Intelligent Field Extraction
GPT-4 intelligently extracts 8 key fields: contact info, work history with dates, highlights, education, skills, certifications, salary expectations, and availability. Handles diverse resume formats and styles.

### Multi-Channel Support
Customize pipelines for Gmail, LinkedIn messages, Indeed applications, or direct email submissions. Route different sources to different Airtable views or workflows.

### Drive + Airtable Sync
Original PDFs stored in Google Drive with organized folder structure. Metadata and extracted fields sync to Airtable for sorting, filtering, and pipeline stage tracking.

### Searchable Pipeline
Airtable views enable filtering by skills, experience level, salary band, or status. Enables team collaboration on candidate scoring and interview scheduling.

## Results

- **3 Screenshots**: Full workflow and Airtable base organization
- **8.5/10 Rating**: Proven effectiveness for startup and agency recruiting
- **6-Step Automation**: Complete from email to organized pipeline
- **8 Extracted Fields**: Rich data enables sophisticated filtering
- **Zero Manual Data Entry**: Candidate data auto-populated from resumes

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/resume-parser-airtable)*
