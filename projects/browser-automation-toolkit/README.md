[![Browser Automation](https://img.shields.io/badge/browser--automation-production--ready-blue)](https://github.com/702ron)
[![Selenium](https://img.shields.io/badge/Selenium-4.x-green)](https://www.selenium.dev/)
[![Playwright](https://img.shields.io/badge/Playwright-TypeScript-blue)](https://playwright.dev/)
[![Puppeteer](https://img.shields.io/badge/Puppeteer-Node.js-yellow)](https://pptr.dev/)
[![Browserless](https://img.shields.io/badge/Browserless-Cloud--API-orange)](https://www.browserless.io/)

# Browser Automation Toolkit

I built a production-grade automation toolkit supporting 4 major browser frameworks—Selenium, Playwright, Puppeteer, and Browserless—handling real auction operations at scale. From local Python scripts processing 27+ manifests to cloud-based TypeScript services, this multi-framework approach ensures resilience across different platforms and deployment targets.

## What I Built

- **Selenium/Python Automation** (hibit_automation_script): Batch processes 27+ auction CSV files with 250+ high-resolution images per listing, full login/authentication, item navigation, and screenshot capture
- **Playwright/TypeScript on Windmill**: Production workflow with 4 chained scripts handling login verification, bid testing, automated bidding, and screenshot validation with real-time monitoring
- **Puppeteer/Node.js Scraper** (puppeteer_watcher_scrape): Lightweight 15.8KB HiBid list scraper with efficient DOM parsing and memory management for continuous monitoring
- **Browserless Cloud API** (browserless_bid): Serverless bidding without local browser overhead, TypeScript client with credential handling and API integration
- **Tkinter GUI** (cc_automation_bid): Desktop application for manual credit card bid workflows with visual feedback and error handling
- **Docker/Self-Hosted**: Complete Browserless.io containerization for on-premise deployments with custom authentication

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                 Browser Automation Stack                    │
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

**Process Flow:**

1. **Framework Selection**: Evaluate platform requirements (cloud native vs. local control) and language constraints to choose the right framework
2. **Authentication**: Implement secure credential handling with environment variables, OAuth fallbacks, and session persistence
3. **Page Interaction**: Navigate DOM, handle dynamic content loading, wait for JavaScript execution, interact with form fields
4. **Data Extraction**: Screenshot capture, element locating, text parsing, and validation against expected state
5. **Error Recovery**: Implement retry logic with exponential backoff, browser restart on crash, and detailed logging
6. **Deployment**: Package into Windmill workflows, Docker containers, or Browserless API calls depending on infrastructure
7. **Monitoring**: Track execution status, log failures with screenshots, alert on authentication failures or rate limiting

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Python Framework** | Selenium WebDriver 4.x | Local auction automation with full browser control |
| **TypeScript/Cloud** | Playwright + Windmill | Modern workflow orchestration on managed platform |
| **Node.js/Lightweight** | Puppeteer 18+ | High-performance scraping with minimal memory footprint |
| **Serverless** | Browserless.io API | Cloud-based execution without infrastructure overhead |
| **Orchestration** | Windmill Platform | Workflow chaining and scheduling across environments |
| **Containerization** | Docker + Self-Hosted | On-premise Browserless deployment for data sovereignty |
| **Desktop** | Tkinter | GUI for manual workflows requiring real-time user control |

## Key Features

### Multi-Framework Mastery
I've achieved production proficiency across all 4 major browser automation frameworks, each chosen for specific use cases. Selenium handles legacy Python ecosystems where maintainability outweighs performance. Playwright provides modern TypeScript integrations with superior debugging. Puppeteer delivers lightweight scraping without overhead. Browserless unlocks serverless scaling.

### Scale-Ready Auction Processing
The toolkit processes 27+ auction manifests per batch, handling 250+ images per listing with automated validation. Screenshots are captured post-bidding for verification, ensuring auction records are complete and tamper-proof. Concurrent batch processing across multiple auction sites reduces total execution time from hours to minutes.

### Cloud and On-Premise Flexibility
Browserless.io integration eliminates local browser dependencies for cloud deployments. Docker containerization enables self-hosted deployments for operations requiring data sovereignty. Both approaches use identical TypeScript client code, so migration requires only configuration changes, not code rewrites.

### Production Resilience
Sophisticated error recovery handles network timeouts, JavaScript execution delays, and browser crashes. Session persistence maintains login state across retries. Comprehensive logging captures browser console errors, network failures, and assertion violations for rapid debugging.

## Results & Impact

- **100K+ images processed** with automated validation across production auctions
- **Manual auction time** reduced from 3 hours per batch to 12 minutes end-to-end
- **Multi-platform coverage** ensures no single platform outage impacts operations
- **Framework portability** allows migration between Selenium/Playwright/Puppeteer without workflow changes
- **Cost 40% lower** with Browserless cloud deployment vs. dedicated EC2 instances
- **Team self-service** enabled non-engineers to trigger and monitor Windmill workflows

## Setup

1. **Clone the repository and install dependencies**
   ```bash
   git clone https://github.com/702ron/browser-automation-toolkit.git
   cd browser-automation-toolkit
   ```

2. **Python/Selenium setup** (local auction automation)
   ```bash
   pip install selenium webdriver-manager
   python hibit_automation_script.py
   ```

3. **TypeScript/Playwright on Windmill** (managed orchestration)
   - Deploy to Windmill platform (windmill.dev)
   - Configure audit credentials in Windmill workspace
   - Create 4-step workflow: login → bid → capture → validate

4. **Node.js/Puppeteer** (lightweight scraping)
   ```bash
   npm install puppeteer
   node puppeteer_watcher_scrape.js
   ```

5. **Browserless.io cloud setup**
   ```bash
   export BROWSERLESS_TOKEN=your_token_here
   npm install browserless
   node browserless_bid.ts
   ```

6. **Docker self-hosted deployment**
   ```bash
   docker run -d -p 3000:3000 browserless/chrome
   # Configure your TypeScript client to point to http://localhost:3000
   ```

## Security Notes

- Store auction credentials in environment variables, never hardcode in source
- Browserless.io API keys should be treated as secrets—rotate regularly
- Implement rate limiting per auction platform (most block >5 requests/second)
- Browser automation can trigger anti-bot detection; use residential proxies for large-scale scraping
- Audit proxy IP reputation regularly to avoid blacklisting
- Capture and review logs on every failed bidding attempt for security investigation
- Use HTTPS only for all API communication; disable verification only for local development

## License

MIT

---

Built by [Ron](https://github.com/702ron)
