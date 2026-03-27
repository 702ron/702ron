# Resume Parser for Airtable

![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) ![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white) ![Airtable](https://img.shields.io/badge/Airtable-F7D563?style=flat&logo=airtable&logoColor=black)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/resume-parser-airtable)**

Automated recruitment pipeline that monitors Gmail for resume attachments, extracts and parses them with GPT-4, and populates Airtable and Google Drive. Processes candidate contact info, work history, key highlights, and 5 additional fields for instant organization and searchability.

## What I Built

- **Gmail Monitoring** - Continuously watches inbox for resume attachments without manual downloads
- **Intelligent PDF Parsing** - GPT-4 extracts 8 structured fields from diverse resume formats and styles
- **8 Extracted Fields** - Contact info, work history (with dates), highlights, education, skills, certifications, salary expectations, availability
- **Google Drive Archival** - Stores original PDFs with organized folder structure for compliance and reference
- **Airtable Base Sync** - Auto-populates spreadsheet with extracted metadata for sorting, filtering, and pipeline management
- **Multi-Channel Support** - Customize pipelines for Gmail, LinkedIn messages, Indeed applications, or direct submissions
- **Searchable Pipeline** - Airtable views enable filtering by skills, experience level, salary band, or stage
- **Zero Manual Data Entry** - Candidate data auto-populated; no copy-paste required
- **3 Comprehensive Screenshots** - Workflow diagrams and Airtable base organization

## Architecture

```
Gmail Monitoring
(Label: Applications)
        ↓
Attachment Extraction
        ↓
GPT-4 Resume Parsing
(8 Structured Fields)
        ↓
   ┌────┴────┬──────────────┐
   ↓         ↓              ↓
Google    Airtable    PostgreSQL
Drive     (Pipeline)   (Backup)
(Archive)
```

**Process Flow:**
1. n8n checks Gmail inbox on schedule
2. Finds emails with resume attachments in target label
3. Extracts PDF attachment
4. Sends to GPT-4 with structured extraction prompt
5. GPT-4 returns 8-field JSON (contact, work history, skills, etc.)
6. Save PDF to Google Drive with folder structure
7. Create/update Airtable record with extracted fields + Drive link
8. Mark email as processed
9. Repeat on next scheduled run

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Email Source** | Gmail API | Resume attachment monitoring |
| **Parser** | OpenAI GPT-4 | Intelligent field extraction |
| **CRM/Database** | Airtable | Candidate pipeline and filtering |
| **File Storage** | Google Drive API | PDF archival and compliance |
| **Orchestration** | n8n | Scheduling, multi-step workflows |
| **Backup** | PostgreSQL (optional) | Long-term audit logs |

## Key Features

### Intelligent Field Extraction
GPT-4 intelligently extracts 8 key fields: contact info, work history with dates, highlights, education, skills, certifications, salary expectations, and availability. Handles diverse resume formats—Word, PDF, Google Docs—without reformatting.

### Multi-Channel Support
Customize pipelines for Gmail, LinkedIn messages, Indeed applications, or direct email submissions. Route different sources to different Airtable views or custom workflows for team-specific handling.

### Drive + Airtable Sync
Original PDFs stored in Google Drive with organized folder structure by date/candidate. Extracted metadata syncs to Airtable for sorting, filtering, and pipeline stage tracking without duplication.

### Searchable Pipeline
Airtable views enable filtering by skills, experience level, salary band, or hiring stage. Enables team collaboration on candidate scoring, interview scheduling, and offer tracking.

## Setup

Complete n8n workflow export, Gmail API setup, Airtable base template, Google Drive integration, and multi-channel customization guide are available in the [full repository](https://github.com/702ron/resume-parser-airtable).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/resume-parser-airtable)*
