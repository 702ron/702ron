![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white) ![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=flat&logo=graphql&logoColor=white)

# Open-Source n8n Community Node — Plain.com Customer Support

**[Full Repository](https://github.com/702ron/n8n-plain-node)** · **[npm Package](https://www.npmjs.com/package/n8n-nodes-plain)**

Open-source n8n community node for Plain.com customer support platform. Full GraphQL API integration covering 6 resources with CRUD operations and real-time event triggers. Published to npm, installable directly in any n8n instance.

## What I Built

- **6-Resource Coverage** — Customers, Conversations, Inboxes, Settings, Thread Attachments, Events
- **Full CRUD Operations** — Create, read, update, delete across all Plain.com resources
- **Trigger Node** — Real-time event subscriptions via GraphQL without polling
- **TypeScript First** — Fully typed with IDE autocomplete and compile-time safety
- **Published to npm** — `npm install n8n-nodes-plain` — installs as a community node

## Architecture

```
n8n Workflow
     ↓
Plain Node Interface (CRUD Operations)
     ↓
GraphQL Query Builder
     ↓
Plain.com GraphQL API
     ↓
   ┌─┴──┬────────┬───────┬─────────┬──────────┬────────┐
   ↓    ↓        ↓       ↓         ↓          ↓        ↓
Customers Conversations Inboxes Settings Attachments Events
```

## Results

- **6 resources** with complete CRUD coverage
- **Real-time triggers** — no polling, instant event-driven workflows
- **npm published** — community-installable, independent of n8n core releases
- **TypeScript** — fully typed, zero runtime type errors

## Tech Stack

TypeScript, n8n Community Nodes SDK, GraphQL, Jest

---

Built by [Ron](https://github.com/702ron)
