# Job Scraper with AI Scoring

Multi-Platform Job Intelligence — Scrape job listings from 8+ platforms and rank them by AI relevance scoring.

## Problem

Job seekers face information overload: Indeed, LinkedIn, Glassdoor, and 5+ other platforms each have unique listings. Aggregating, deduplicating, and ranking jobs by actual fit requires manual effort or expensive subscription services. An intelligent scraper that ranks jobs by relevance using AI can dramatically improve the job search experience.

## Solution

Built **jobspy**, a Flask web application that scrapes job listings from 8+ platforms and uses AI to score and rank them:

**Core Components:**
- **app.py** (24KB): Flask web server with routes for searching, filtering, and browsing
- **job_scorer.py** (4.3KB): AI-based job evaluation using semantic analysis
- **job_tracker.py** (8.6KB): SQLite persistence with 2MB of real job data
- **jsearch_client.py** (2.7KB): JSearch API wrapper for data enrichment

**Supported Platforms:**
- Indeed, Glassdoor, LinkedIn, ZipRecruiter, Google Jobs, Naukri, BDJobs, Bayt
- Unified schema across all platforms
- Deduplication across sources

**Technology:**
- Python 3.9+ with Poetry dependency management
- Flask for web framework
- SQLite for job data persistence (2MB+ historical data)
- OpenAI for job scoring and relevance ranking
- Multi-threaded scraping for performance

```
┌─────────────────────────────────────────────────────────────┐
│            Job Scraper AI Scoring Architecture              │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  User Interface (Flask Web App)                             │
│  ┌──────────────────────────────────────┐                  │
│  │  Flask Routes:                       │                  │
│  │  - GET /search (query + filters)     │                  │
│  │  - GET /jobs (list with pagination)  │                  │
│  │  - GET /job/<id> (detail view)       │                  │
│  │  - POST /score (trigger rescoring)   │                  │
│  │  - GET /dashboard (stats & charts)   │                  │
│  └──────────────────────────────────────┘                  │
│         │                                                    │
│         ▼                                                    │
│  ┌──────────────────────────────────────┐                  │
│  │  Multi-Platform Scraper (Sequential) │                  │
│  │                                      │                  │
│  │  Platform Scrapers:                  │                  │
│  │  ├─ Indeed Scraper                   │                  │
│  │  ├─ LinkedIn Scraper                 │                  │
│  │  ├─ Glassdoor Scraper                │                  │
│  │  ├─ ZipRecruiter Scraper             │                  │
│  │  ├─ Google Jobs Scraper              │                  │
│  │  ├─ Naukri Scraper (India)           │                  │
│  │  ├─ BDJobs Scraper (Bangladesh)      │                  │
│  │  └─ Bayt Scraper (Middle East)       │                  │
│  │                                      │                  │
│  │  jsearch_client.py (API Wrapper)     │                  │
│  │  └─ Data enrichment & standardization│                  │
│  └──────────────────────────────────────┘                  │
│         │                                                    │
│         ▼                                                    │
│  ┌──────────────────────────────────────┐                  │
│  │  Job Deduplication                   │                  │
│  │  - Hash similar listings              │                  │
│  │  - Merge duplicate entries            │                  │
│  │  - Keep source references             │                  │
│  └──────────────────────────────────────┘                  │
│         │                                                    │
│         ▼                                                    │
│  ┌──────────────────────────────────────┐                  │
│  │  AI Job Scoring Pipeline             │                  │
│  │  job_scorer.py (4.3KB)               │                  │
│  │                                      │                  │
│  │  Score Factors:                      │                  │
│  │  ├─ Skill match (skills vs job req)  │                  │
│  │  ├─ Location relevance                │                  │
│  │  ├─ Salary alignment                  │                  │
│  │  ├─ Company prestige (OpenAI)         │                  │
│  │  ├─ Role level match (junior/senior) │                  │
│  │  └─ Remote flexibility                │                  │
│  │                                      │                  │
│  │  Returns: 0-100 relevance score      │                  │
│  └──────────────────────────────────────┘                  │
│         │                                                    │
│         ▼                                                    │
│  ┌──────────────────────────────────────┐                  │
│  │  SQLite Storage (2MB+ historical)    │                  │
│  │  job_tracker.py (8.6KB)              │                  │
│  │                                      │                  │
│  │  Tables:                             │                  │
│  │  ├─ jobs (title, desc, salary)       │                  │
│  │  ├─ job_scores (relevance rating)    │                  │
│  │  ├─ applications (user applications) │                  │
│  │  └─ source_urls (dedupe across sites)│                  │
│  └──────────────────────────────────────┘                  │
│         │                                                    │
│         ▼                                                    │
│  Ranked Results (Sorted by AI Score)                       │
│  - "Python Developer" at TechCorp (89/100)                 │
│  - "Backend Engineer" at StartupXYZ (82/100)               │
│  - "Software Engineer" at Boring Corp (45/100)             │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Language** | Python 3.9+ | Core application |
| **Web Framework** | Flask | HTTP server & routing |
| **Data Storage** | SQLite | Job listings & historical data |
| **Dependency Mgmt** | Poetry | Package management |
| **Web Scraping** | Beautiful Soup, Requests | HTML parsing & HTTP |
| **AI Scoring** | OpenAI GPT-4 | Job relevance evaluation |
| **APIs** | JSearch, platform-specific | Job data enrichment |
| **Concurrency** | Threading, asyncio | Multi-platform scraping |

## Key Features

### Multi-Platform Scraping
- 8+ job boards integrated (Indeed, LinkedIn, Glassdoor, etc.)
- Unified schema across disparate data sources
- Automatic deduplication of cross-platform listings
- Source tracking for job application workflow
- Handles regional platforms (Naukri, BDJobs, Bayt)

### AI-Powered Job Scoring
- OpenAI semantic analysis of job descriptions
- Multi-factor scoring:
  - Skill match against job requirements
  - Location fit and remote flexibility
  - Salary alignment with market rates
  - Company prestige and reputation
  - Role level (junior/mid/senior) matching
- Produces 0-100 relevance score per job
- Enables personalized job ranking

### Data Persistence & Analytics
- 2MB+ of historical job data in SQLite
- Job tracker with application status
- Score history for trend analysis
- Search filtering by score range, salary, location
- Dashboard statistics and visualizations

### Production-Ready Codebase
- Clean separation: scraping, scoring, tracking, API
- Poetry for reproducible environments
- Error handling and retry logic
- Logging for debugging
- Flask templating for simple web UI

## Results & Impact

- **Reduced job search time** from hours browsing 8 sites to minutes browsing ranked results
- **Improved application quality** by focusing on jobs with highest relevance scores
- **Cross-platform aggregation** eliminates duplicate job hunting effort
- **Historical job tracking** enables trend analysis and market intelligence
- **Scalable architecture** supporting 2MB+ historical data
- **Personalized recommendations** through AI scoring

## License

MIT

---

Built by [Ron](https://github.com/702ron)
