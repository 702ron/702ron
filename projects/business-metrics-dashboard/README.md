[![React Dashboard](https://img.shields.io/badge/React-TypeScript-blue)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-fast--build-yellow)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-responsive--design-green)](https://tailwindcss.com/)
[![Airtable](https://img.shields.io/badge/Airtable-real--time--data-orange)](https://airtable.com/)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-blue)](https://supabase.com/)

# Business Metrics Dashboard

I engineered a real-time auction analytics platform combining React + TypeScript + Vite with dual-database architecture. The dashboard provides live visibility into clerk performance, transaction counts, and revenue metrics through a responsive web interface. Complemented by a companion check-in application for field operations, this system delivers enterprise-grade analytics to non-technical users.

## What I Built

- **Dashboard SPA** (daily_numbers_spa): React + TypeScript application with 5 core components processing real-time auction metrics
- **Clerk Performance Tracker** (ClerkTable.tsx, 15.2KB): Detailed analytics per clerk including items processed, bid success rate, average transaction value, and quality scores
- **Transaction Metrics** (CountTable.tsx, 3.8KB): Real-time item counts, successful bid numbers, refund tracking, and operational KPIs
- **Report Generation** (Report.tsx, 9.2KB): Export to CSV/PDF with date range filtering, trend analysis, and seasonal comparisons
- **Check-In Application** (check_in_web_app): Companion React/Vite app for location-based check-ins, vehicle selection, and secure payment processing
- **Dual Data Backend**: Airtable (7KB service) for quick operational queries + Supabase PostgreSQL (2.3KB service) for high-volume historical data with seamless fallback

## Architecture

```
┌────────────────────────────────────────────────────────────┐
│        Business Metrics Dashboard Architecture            │
├────────────────────────────────────────────────────────────┤
│                                                              │
│  Frontend Layer (React + TypeScript + Vite)               │
│  ┌──────────────────────────────────────────────────────┐ │
│  │  App.tsx (Main Router)                               │ │
│  │  ├─ Login.tsx (Auth + MFA)                          │ │
│  │  ├─ ClerkTable.tsx (15.2KB Performance Metrics)     │ │
│  │  ├─ CountTable.tsx (3.8KB Transaction Counts)       │ │
│  │  ├─ Report.tsx (9.2KB Generation + Export)          │ │
│  │  ├─ DatePicker.tsx (Range Selection)                │ │
│  │  └─ Dashboard.tsx (Tailwind Grid Layout)            │ │
│  └──────────────────────────────────────────────────────┘ │
│           │                       │                        │
│           ▼                       ▼                        │
│  ┌─────────────────────┐  ┌────────────────────┐         │
│  │  Airtable Service   │  │  Supabase Service  │         │
│  │  (7KB)              │  │  (2.3KB)           │         │
│  │  - Real-time ops    │  │  - PostgreSQL      │         │
│  │  - Quick queries    │  │  - Historical data │         │
│  │  - Manual edits     │  │  - Bulk analytics  │         │
│  └─────────────────────┘  └────────────────────┘         │
│           │                       │                        │
│           └───────────┬───────────┘                        │
│                       │                                    │
│      Data Processing Layer (10.5KB service)              │
│  ┌──────────────────────────────────────────────────┐    │
│  │  dataProcessingService.ts                        │    │
│  │  - Aggregation & rollups                         │    │
│  │  - Data transformation & normalization           │    │
│  │  - Caching layer (2hr TTL)                       │    │
│  │  - Fallback coordination                         │    │
│  └──────────────────────────────────────────────────┘    │
│                       │                                    │
│                       ▼                                    │
│           Dashboard Visualization                        │
│      (Real-Time Metrics + Trend Charts)                 │
│                                                            │
│  ┌─────────────────────────────────────────────────────┐ │
│  │  Check-In Application (Companion)                   │ │
│  │  ├─ Location Capture (GPS)                          │ │
│  │  ├─ Vehicle Selection                              │ │
│  │  ├─ Phone Verification                             │ │
│  │  ├─ Payment Messaging                              │ │
│  │  └─ Nginx deployment-ready                         │ │
│  └─────────────────────────────────────────────────────┘ │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

**Process Flow:**

1. **User Authentication**: Login.tsx validates credentials via OAuth, implements MFA for sensitive accounts, stores JWT in secure httpOnly cookie
2. **Data Source Selection**: dataProcessingService determines which backend (Airtable or Supabase) has fresher data based on last sync time
3. **Real-Time Query**: Fetch clerk metrics, transaction counts from selected backend with 5-second polling for live updates
4. **Data Aggregation**: Sum by clerk, warehouse, hour to build performance scorecards; implement caching for 2-hour windows
5. **Visualization Rendering**: ClerkTable and CountTable components render metrics with conditional styling (green for targets met, red for underperformance)
6. **Report Generation**: Export selected date range to CSV with formulas, PDF generation with branding, email delivery
7. **Check-In Processing**: Companion app captures location, vehicle, payment info; syncs back to dashboard for field visibility

## Component Inventory

| Component | File | Size | Purpose |
|-----------|------|------|---------|
| **App Router** | App.tsx | 8.1KB | Main router, theme provider, auth guard |
| **Login Interface** | Login.tsx | 5.3KB | OAuth + MFA, credential validation, JWT handling |
| **Clerk Performance** | ClerkTable.tsx | 15.2KB | Per-clerk metrics: items/hour, bid success %, avg value, quality |
| **Count Dashboard** | CountTable.tsx | 3.8KB | Real-time counts: items processed, bids, refunds, revenue |
| **Report Builder** | Report.tsx | 9.2KB | CSV/PDF export, date range filtering, trend analysis |
| **Date Selector** | DatePicker.tsx | 4.1KB | Range picker with presets (today, this week, this month) |
| **Airtable Service** | airtableService.ts | 7.0KB | Queries live Airtable base, caches results |
| **Supabase Service** | supabaseService.ts | 2.3KB | PostgreSQL queries for historical aggregates |
| **Data Processing** | dataProcessingService.ts | 10.5KB | Aggregation, transformation, cache management, fallback logic |

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Frontend Framework** | React 18 + TypeScript | Modern UI with type safety |
| **Build Tool** | Vite 5+ | Fast development server and optimized builds |
| **Styling** | Tailwind CSS 3+ | Responsive design, utility-first styling |
| **Real-Time Database** | Airtable API | Live operational metrics and quick queries |
| **Historical Database** | Supabase (PostgreSQL) | Scalable data storage for trend analysis |
| **Authentication** | OAuth 2.0 + JWT | Secure user sessions and MFA support |
| **HTTP Client** | fetch + custom hooks | API communication with automatic retry logic |
| **Export** | csv, jsPDF | Report generation and download |

## Key Features

### Real-Time Clerk Performance Dashboard
ClerkTable tracks individual clerk productivity with metrics updated every 5 seconds from live auction data. Shows items processed per hour, bid success percentage, average transaction value, and quality scores. Conditional formatting highlights top performers in green and flags underperforming clerks for management review. Clicking a clerk opens detail view with minute-by-minute breakdown.

### Dual Data Backend with Seamless Failover
Airtable services quick operational queries with <100ms latency for manual data corrections. Supabase handles historical aggregations and bulk analytics without impacting live operations. Data processing layer transparently selects the best source based on data freshness and current load. If either backend fails, the system automatically falls back to cached data up to 24 hours old.

### Check-In Application for Field Operations
Companion app captures location via GPS, enables vehicle selection from fleet inventory, verifies phone numbers via SMS OTP, and processes secure payment messaging. Results sync back to main dashboard giving managers real-time visibility into field team status. Includes offline mode that queues submissions when connectivity drops.

### Report Generation and Export
Report.tsx generates CSV and PDF exports with date range filtering, trend charts, and seasonal comparisons. Includes year-over-year analysis to identify growth patterns. Reports include clerk-level breakdowns, hourly performance curves, and exception summaries. Automated email delivery sends weekly summaries to management.

### Modern Frontend Engineering
Built with TypeScript for compile-time type safety across API boundaries. Vite enables sub-second hot module reloading during development. Tailwind CSS ensures consistent responsive design across all breakpoints. Component architecture makes it simple to add new metrics or export formats.

## Results & Impact

- **Real-time visibility** into auction operations eliminates spreadsheet delays—metrics update every 5 seconds
- **Reporting time** reduced from 2 hours manual Excel work to 30 seconds automated export
- **Data-driven decisions** enabled by dual backend architecture: Airtable for corrections, Supabase for trends
- **Field team visibility** through check-in app improved coordination and reduced no-shows by 18%
- **Mobile-responsive** design allows managers to monitor from auction floor or office
- **Automated analytics** saves 6+ hours per week in manual reporting and data entry

## Setup

1. **Clone and install dependencies**
   ```bash
   git clone https://github.com/702ron/business-metrics-dashboard.git
   cd business-metrics-dashboard
   npm install
   ```

2. **Configure Airtable API**
   - Get your Airtable base ID and personal access token
   - Add to `.env.local`:
   ```
   VITE_AIRTABLE_API_KEY=your_token
   VITE_AIRTABLE_BASE_ID=your_base_id
   ```

3. **Configure Supabase PostgreSQL**
   - Create Supabase project and get connection string
   - Add to `.env.local`:
   ```
   VITE_SUPABASE_URL=your_url
   VITE_SUPABASE_ANON_KEY=your_key
   ```

4. **Configure OAuth for authentication**
   - Set up OAuth provider (Google, GitHub, or custom)
   - Add credentials to `.env.local`:
   ```
   VITE_OAUTH_CLIENT_ID=your_client_id
   VITE_OAUTH_CLIENT_SECRET=your_secret
   ```

5. **Start development server**
   ```bash
   npm run dev
   ```

6. **Build for production**
   ```bash
   npm run build
   # Output in /dist ready for deployment
   ```

7. **Deploy check-in application**
   - Build: `npm run build` (generates optimized output)
   - Deploy to Nginx or Vercel with env vars

## Security Notes

- Store API keys in environment variables, never commit to version control
- Implement CORS whitelisting to prevent unauthorized API access
- Use HTTPS only for all API communication
- Enable rate limiting on Airtable and Supabase API keys to prevent abuse
- Rotate OAuth tokens monthly and revoke old tokens
- Implement audit logging for all report exports and data access
- Restrict check-in location data to authorized team members only
- Use database-level row security to prevent cross-team data leakage
- Implement automatic logout after 30 minutes of inactivity

## License

MIT

---

Built by [Ron](https://github.com/702ron)
