![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) ![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white) ![Airtable](https://img.shields.io/badge/Airtable-F7D563?style=flat&logo=airtable&logoColor=black)

# Automated Resume Parsing — Gmail to Airtable Pipeline

**[Full Repository](https://github.com/702ron/resume-parser-airtable)**

Automated recruitment pipeline that monitors Gmail for resume attachments, extracts 8 structured fields with GPT-4, archives PDFs to Google Drive, and populates a searchable Airtable candidate tracker. Zero manual data entry.

![n8n Workflow](https://raw.githubusercontent.com/702ron/resume-parser-airtable/main/screenshots/n8n_workflow.png)

## What I Built

- **Gmail Monitoring** — Continuously watches inbox for resume attachments without manual downloads
- **GPT-4 Field Extraction** — Parses 8 fields: contact info, work history, highlights, education, skills, certifications, salary, availability
- **Google Drive Archival** — Organized folder structure for compliance and reference
- **Airtable Pipeline** — Searchable candidate tracker with filtering by skills, experience, salary band
- **Multi-Channel Support** — Customize for Gmail, LinkedIn, Indeed, or direct submissions

## Screenshots

![Airtable View](https://raw.githubusercontent.com/702ron/resume-parser-airtable/main/screenshots/airtable.png)

## Architecture

```
Gmail Monitoring (Label: Applications)
        ↓
  Attachment Extraction
        ↓
  GPT-4 Resume Parsing (8 Fields)
        ↓
   ┌────┴────┬──────────┐
   ↓         ↓          ↓
Google    Airtable   PostgreSQL
Drive     (Pipeline)  (Backup)
(Archive)
```

## Results

- **8 structured fields** extracted per resume automatically
- **Zero manual data entry** — candidates flow from inbox to pipeline
- **Searchable Airtable views** for filtering by skills, experience, salary
- **Multi-channel** — works with Gmail, LinkedIn, Indeed, direct email

## Tech Stack

n8n, OpenAI GPT-4, Gmail API, Google Drive API, Airtable

---

Built by [Ron](https://github.com/702ron)
