[![React Dashboard](https://img.shields.io/badge/React-TypeScript-blue)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-fast--build-yellow)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-responsive--design-green)](https://tailwindcss.com/)
[![Airtable](https://img.shields.io/badge/Airtable-real--time--data-orange)](https://airtable.com/)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-blue)](https://supabase.com/)

# Real-Time Analytics for 4,000+ Monthly Auctions

I engineered a real-time auction analytics platform combining React + TypeScript with dual-database architecture (Airtable for live operations, Supabase for historical trends). The dashboard provides instant visibility into clerk performance, transaction metrics, and revenue—cutting reporting time from 2 hours of manual Excel work to 30 seconds of automated export.

## What I Built

- **React Dashboard** with 5 core components processing real-time metrics and rendering clerk performance, transaction counts, and trend analysis
- **Dual Backend** — Airtable (7KB service) for quick operational queries + Supabase PostgreSQL (2.3KB service) for high-volume historical data with seamless fallback
- **Report Generation** — Export to CSV/PDF with date range filtering, trend analysis, and seasonal comparisons
- **Check-In Application** — Companion React/Vite app for field teams with GPS location capture, vehicle selection, and payment messaging
- **Data Processing Layer** (10.5KB) — Aggregation, transformation, 2-hour caching, and intelligent fallback coordination

## Architecture

```
Frontend Layer (React + TypeScript + Vite)
├─ App.tsx (Main Router + Auth Guard)
├─ ClerkTable.tsx (Per-clerk performance metrics)
├─ CountTable.tsx (Real-time transaction counts)
├─ Report.tsx (CSV/PDF export)
└─ Dashboard.tsx (Tailwind grid layout)
       │
       ├─ Airtable Service (Real-time ops)
       └─ Supabase Service (Historical data)
              │
       Data Processing Layer
       (Aggregation, Caching, Fallback)
              │
       Live Dashboard + Check-In App
```

## Results

| Metric | Impact |
|--------|--------|
| **Reporting time** | 2 hours → 30 seconds (automated export) |
| **Metrics latency** | 5-second polling for live updates |
| **Field visibility** | Check-in app reduced no-shows by 18% |
| **Clerk insights** | Individual minute-by-minute breakdown available |
| **Weekly savings** | 6+ hours of manual reporting eliminated |

## Tech Stack

React 18 + TypeScript | Vite | Tailwind CSS | Airtable API | Supabase PostgreSQL | OAuth 2.0 + JWT

<!-- Screenshots: Dashboard showing real-time clerk performance metrics, transaction counts, and date range report export. -->

---

Built by [Ron](https://github.com/702ron)
