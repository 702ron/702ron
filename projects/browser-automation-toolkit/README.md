[![Browser Automation](https://img.shields.io/badge/browser--automation-production--ready-blue)](https://github.com/702ron)
[![Selenium](https://img.shields.io/badge/Selenium-4.x-green)](https://www.selenium.dev/)
[![Playwright](https://img.shields.io/badge/Playwright-TypeScript-blue)](https://playwright.dev/)
[![Puppeteer](https://img.shields.io/badge/Puppeteer-Node.js-yellow)](https://pptr.dev/)
[![Browserless](https://img.shields.io/badge/Browserless-Cloud--API-orange)](https://www.browserless.io/)

# Automated 100K+ Images Across 4 Browser Frameworks—From 3 Hours to 12 Minutes

I engineered a production-grade automation toolkit supporting Selenium, Playwright, Puppeteer, and Browserless—handling real auction operations at scale. The multi-framework approach ensures resilience: if one platform fails, operations continue seamlessly. Processes 27+ auction manifests with 250+ high-resolution images per listing, handling login, bidding, screenshot capture, and validation end-to-end.

## What I Built

- **Selenium/Python Automation** — Batch processes 27+ CSV auction files with full authentication, item navigation, and screenshot capture
- **Playwright/TypeScript on Windmill** — Production workflow with 4 chained steps (login, bid, screenshot, validate) running on managed platform
- **Puppeteer/Node.js Scraper** — Lightweight 15.8KB HiBid list monitor with efficient DOM parsing for continuous auction tracking
- **Browserless Cloud API** — Serverless bidding without local browser overhead; TypeScript client with credential handling
- **Tkinter Desktop GUI** — Manual credit card bid workflows with visual feedback and error handling
- **Docker Self-Hosted** — Complete Browserless containerization for on-premise deployments with custom authentication

## Architecture

```
Selenium (Python)    Playwright (TS)    Puppeteer (Node)
      │                   │                    │
      └──────────────┬────┴────────────┬──────┘
                     │                 │
          HiBid Auctions        Windmill Platform
                     │                 │
                     └────────┬────────┘
                              │
                    Browserless.io Cloud API
                              │
                    ┌─────────┴──────────┐
                    │                    │
              Docker Container    Local Browser
          (Self-Hosted Service)   (Dev/Testing)
```

## Results

| Metric | Impact |
|--------|--------|
| **Manual auction time** | 3 hours → 12 minutes per batch (83% faster) |
| **Images processed** | 100K+ with automated validation |
| **Multi-platform coverage** | Single failure doesn't stop operations |
| **Framework portability** | Migrate Selenium/Playwright/Puppeteer without workflow changes |
| **Cost efficiency** | 40% lower with Browserless cloud vs. EC2 instances |
| **Team self-service** | Non-engineers trigger and monitor workflows |

## Tech Stack

Selenium 4.x + Python | Playwright + TypeScript | Puppeteer 18+ | Browserless.io API | Windmill Platform | Docker | Tkinter

<!-- Screenshots: Browser automation executing auction bidding workflow, screenshot capture showing bid confirmation, and Windmill dashboard tracking execution status. -->

---

Built by [Ron](https://github.com/702ron)
