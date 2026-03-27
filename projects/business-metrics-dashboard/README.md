# Business Metrics Dashboard

Real-Time Auction Analytics — React-based frontend for business intelligence and operational metrics.

## Problem

Auction operations generate real-time data (clerk performance, item counts, revenue metrics) that requires immediate visualization for decision-making. Building a dashboard that can scale from ad-hoc queries to production monitoring requires a modern frontend with dual-data backend support, responsive design, and smooth performance.

## Solution

Built **daily_numbers_spa**, a React + TypeScript + Vite + Tailwind CSS application with real-time data visualization:

- **ClerkTable.tsx** (15.2KB): Performance metrics for auction clerks
- **CountTable.tsx** (3.8KB): Item and transaction count dashboards
- **Report.tsx** (9.2KB): Report generation and export
- **DatePicker.tsx**: Custom date range selection
- **Login.tsx**: Authentication interface

**Dual Data Backend:**
- Airtable service (7KB): Real-time Airtable base queries
- Supabase service (2.3KB): PostgreSQL fallback for high-volume data
- Data processing service (10.5KB): Transformation and aggregation

Also built **check_in_web_app**, a complementary React/Vite application for location-based check-ins with vehicle selection, phone verification, and secure payment messaging.

```
┌────────────────────────────────────────────────────────────┐
│            Business Metrics Dashboard Architecture         │
├────────────────────────────────────────────────────────────┤
│                                                              │
│  Frontend Layer (React + TypeScript + Vite)                │
│  ┌──────────────────────────────────────────────────┐      │
│  │  App.tsx (Main)                                  │      │
│  │  ├─ Login.tsx (Auth)                             │      │
│  │  ├─ ClerkTable.tsx (15.2KB Performance)          │      │
│  │  ├─ CountTable.tsx (3.8KB Counts)                │      │
│  │  ├─ Report.tsx (9.2KB Generation)                │      │
│  │  ├─ DatePicker.tsx (Range Selection)             │      │
│  │  └─ UI Components (Tailwind Styled)              │      │
│  └──────────────────────────────────────────────────┘      │
│           │                      │                          │
│           ▼                      ▼                          │
│  ┌─────────────────┐    ┌────────────────┐                │
│  │  Airtable API   │    │ Supabase API   │                │
│  │  (Real-Time)    │    │ (PostgreSQL)   │                │
│  └─────────────────┘    └────────────────┘                │
│           │                      │                          │
│           └──────────┬───────────┘                          │
│                      │                                      │
│          Data Processing Layer                             │
│  ┌──────────────────────────────────────┐                 │
│  │ dataProcessingService.ts (10.5KB)   │                 │
│  │ - Aggregation                        │                 │
│  │ - Transformation                     │                 │
│  │ - Caching                            │                 │
│  └──────────────────────────────────────┘                 │
│                      │                                      │
│                      ▼                                      │
│            Dashboard Visualization                         │
│            (Real-Time Metrics)                             │
│                                                              │
└────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Frontend** | React, TypeScript, Vite | Modern UI framework |
| **Styling** | Tailwind CSS | Responsive design system |
| **Database 1** | Airtable API | Real-time metric queries |
| **Database 2** | Supabase (PostgreSQL) | Scalable data storage |
| **Services** | Node.js | Backend API support |
| **Package Manager** | npm/yarn | Dependency management |

## Key Features

### Real-Time Metrics Dashboard
- Clerk performance tracking with detailed analytics
- Item count and transaction metrics
- Custom date range selection
- Live data refresh from dual sources
- Report generation and export functionality

### Dual Data Backend Architecture
- Airtable for quick operational queries and manual data entry
- Supabase PostgreSQL for high-volume historical data and aggregations
- Fallback mechanisms between backends for reliability
- Data processing layer handles normalization and caching

### Check-In Application
- Location-based check-in with GPS capture
- Vehicle selection from fleet inventory
- Phone number verification
- Payment messaging and notifications
- Secure authentication middleware
- Nginx deployment-ready configuration

### Modern Frontend Engineering
- TypeScript for type safety and maintainability
- Vite for fast development and optimized builds
- Tailwind CSS for consistent responsive design
- Reusable component architecture
- API service layer abstraction

## Results & Impact

- **Real-time visibility** into auction clerk performance metrics
- **Reduced reporting time** from manual Excel sheets to instant dashboards
- **Dual database flexibility** allowing seamless scaling as data volume grows
- **Mobile-responsive design** enables check-in from field locations
- **Automated report generation** saves 30+ minutes per week
- **Team confidence** with accurate, real-time operational metrics

## License

MIT

---

Built by [Ron](https://github.com/702ron)
