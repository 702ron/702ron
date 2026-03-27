# Browser Automation Toolkit

Selenium, Playwright, Puppeteer & Browserless — A collection of battle-tested browser automation scripts across 4 frameworks, all used in production for auction operations.

## Problem

Modern auction platforms require automated interaction at scale: logging in, navigating dynamic content, placing bids, and capturing screenshots for verification. Each platform has different authentication mechanisms and JavaScript rendering requirements. Supporting multiple frameworks and cloud-based alternatives was essential for resilience and cost optimization.

## Solution

Built a modular automation toolkit spanning 4 major browser automation frameworks:

- **Python/Selenium** (hibit_automation_script): Processes 27+ auction CSV files with 250+ images per listing
- **TypeScript/Playwright** (windmill_scraper_v2): Runs on the Windmill platform with auction watcher + auto-bidder logic
- **Node.js/Puppeteer** (puppeteer_watcher_scrape): Lightweight HiBid list scraping at 15.8KB
- **TypeScript/Browserless** (browserless_bid): Cloud-based bidding via Browserless.io API, no local browser needed
- **Python/Tkinter** (cc_automation_bid): GUI for credit card bid automation
- **Docker/Self-Hosted**: Browserless.io service for containerized deployments

```
┌─────────────────────────────────────────────────────────────┐
│                    Browser Automation Stack                 │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  Selenium (Python)    Playwright (TS)    Puppeteer (Node)   │
│      │                      │                    │            │
│      └──────────────┬───────┴────────────┬──────┘            │
│                     │                    │                   │
│          HiBid Auctions         Windmill Platform            │
│                     │                    │                   │
│                     └────────┬───────────┘                   │
│                              │                               │
│                    Browserless.io Cloud API                 │
│                    (TypeScript/Local Fallback)              │
│                              │                               │
│                    ┌─────────┴──────────┐                   │
│                    │                    │                   │
│              Docker Container    Local Browser              │
│          (Self-Hosted Service)   (Dev/Testing)              │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Frameworks** | Selenium, Playwright, Puppeteer | Multi-framework browser control |
| **Cloud** | Browserless.io | Serverless automation via API |
| **Languages** | Python, TypeScript, Node.js | Framework-specific implementations |
| **Platforms** | Windmill, Docker | Orchestration & containerization |
| **UI** | Tkinter | Desktop GUI for credit card automation |
| **Testing** | Login/Bid/Screenshot verification | Quality assurance for each framework |

## Key Features

### Multi-Framework Support
Mastery across all 4 major browser automation frameworks:
- Selenium for Python workflows (industry standard for legacy systems)
- Playwright for modern TypeScript codebases (Windmill integration)
- Puppeteer for Node.js (lightweight, performant scraping)
- Browserless for cloud-based, serverless execution (no infrastructure)

### Production Auction Processing
- Processes 27+ auction CSV files in batch
- Handles 250+ high-resolution images per auction listing
- Automated HiBid list scraping and watcher functionality
- 4-script Windmill pipeline with login, bid testing, and screenshot verification
- Automatic bidding with validation

### Cloud & Local Flexibility
- Browserless.io cloud API for scaling without local browser instances
- Self-hosted Docker deployment option for on-premise control
- Local fallback mechanisms for development and testing
- Zero infrastructure setup for cloud variant

## Results & Impact

- **Reduced manual auction listing time** from hours to minutes per batch
- **Processed 100K+ image uploads** with automated validation
- **Multi-platform coverage**: HiBid, Windmill, and custom auction systems
- **Framework agility**: Easy to swap implementations based on platform requirements
- **Cost optimization**: Cloud variant eliminates local browser overhead
- **Team enablement**: Windmill scripts allow non-engineers to trigger automations

## License

MIT

---

Built by [Ron](https://github.com/702ron)
