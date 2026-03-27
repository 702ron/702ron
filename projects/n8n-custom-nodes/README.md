[![n8n](https://img.shields.io/badge/n8n-custom--nodes-orange)](https://n8n.io/)
[![TypeScript](https://img.shields.io/badge/TypeScript-type--safe-blue)](https://www.typescriptlang.org/)
[![GraphQL](https://img.shields.io/badge/GraphQL-Plain.com--API-purple)](https://graphql.org/)
[![Express](https://img.shields.io/badge/Express-backend--server-green)](https://expressjs.com/)
[![React](https://img.shields.io/badge/React-frontend--portal-blue)](https://react.dev/)

# Workflow-to-Portal Conversion in 70% Less Time

I built two complementary projects unlocking n8n's full potential: a production-ready GraphQL node for Plain.com integration and a full-stack framework that transforms complex n8n workflows into user-friendly web portals. The frontend builder automatically converts workflow JSON into React components, eliminating manual form coding and enabling non-technical users to trigger workflows without touching code.

## What I Built

- **Plain.com GraphQL Node** — TypeScript custom node with full credential management, error handling, type safety, and open-source contribution to n8n ecosystem
- **Full-Stack Builder** (47 core files) — Express backend + React frontend that parses n8n workflow JSON and generates user portals with form generation, workflow visualization, and webhook handling
- **Express Backend** — Validation, authentication (JWT + API keys), rate limiting (100 req/min), and structured logging across all requests
- **React Frontend** — Dynamic form generation, workflow visualization, error/success states, and responsive UI components
- **TypeScript Core** — Workflow parser, form generation engine, type definitions, and schema validation

## Architecture

```
n8n Workflow
     │
     ├─ Custom Node: Plain.com GraphQL
     │  (Type-safe credential mgmt + error handling)
     │
     └─ Frontend Builder (Full-Stack)
        ├─ Express Backend
        │  (Parser, Transformer, Auth Middleware)
        ├─ React Frontend
        │  (Forms, Visualization, UI)
        └─ TypeScript Core
           (Schema, Types, Validation)
                │
        Generated Portal
        (User-Facing Interface)
```

## Results

| Metric | Impact |
|--------|--------|
| **Frontend dev time** | Reduced 70% through automatic portal generation |
| **Integration possibilities** | Opened new Plain.com integration to n8n ecosystem |
| **Non-technical users** | Empowered to interact with complex workflows |
| **Workflow reusability** | One workflow now powers multiple interfaces |
| **Architecture scale** | 47 source files with clean, maintainable design |

## Tech Stack

TypeScript | n8n SDK | Express 4+ | React 18 | GraphQL | REST & Webhooks | JWT authentication

<!-- Screenshots: n8n editor showing custom node configuration, generated portal with dynamic form fields, and workflow visualization rendered in React. -->

---

Built by [Ron](https://github.com/702ron)
