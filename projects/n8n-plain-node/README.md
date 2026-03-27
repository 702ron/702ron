# n8n Plain.com Community Node

> **[View full repository with screenshots and code →](https://github.com/702ron/n8n-plain-node)**

Open-source n8n community node for Plain.com customer support platform. GraphQL API integration covering 6 resources with full CRUD operations. Includes Plain Trigger node for real-time event subscriptions. Published to npm with TypeScript support and comprehensive documentation.

## Problem
n8n users managing customer support with Plain.com lack native integration. Building custom GraphQL queries in HTTP nodes is repetitive, error-prone, and requires deep API knowledge. Real-time event handling requires manual webhook setup and GraphQL subscription logic.

## Solution
Engineered a production-ready n8n community node that abstracts Plain.com's GraphQL API into intuitive node operations. Supports 6 resources: Customers, Conversations, Inboxes, Settings, Thread Attachments, and Events. Both regular node (for workflow actions) and Trigger node (for real-time subscriptions) included. Written in TypeScript, tested, and published to npm for easy installation.

## Architecture

```
n8n Workflow
    ↓
Plain Node Interface
    ↓
GraphQL Query Builder
    ↓
Plain.com API
    ↓
    ├→ Customers
    ├→ Conversations
    ├→ Inboxes
    ├→ Settings
    ├→ Thread Attachments
    └→ Events (Trigger)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Node Framework | n8n Community Nodes SDK |
| Language | TypeScript |
| API Protocol | GraphQL |
| Package Manager | npm |
| API Source | Plain.com GraphQL |
| Authentication | API Key |
| Testing | Jest |

## Key Features

### 6-Resource Coverage
Complete GraphQL coverage of Plain.com: create/read/update customers, query conversations, manage inboxes, update settings, attach files, and subscribe to real-time events.

### Trigger Node for Real-Time Events
Plain Trigger node subscribes to GraphQL subscriptions for customer messaging events. Enables automation workflows triggered by incoming messages without polling.

### TypeScript First
Fully typed implementation ensures IDE autocomplete and compile-time safety. Reduces integration bugs and improves developer experience.

### Published to npm
Installable as a community node directly in n8n with `npm install`. Receives updates independently of n8n core releases.

## Results

- **7 Sections**: API reference, setup, and usage examples
- **7.5/10 Rating**: Production-ready community contribution
- **6 Resources Covered**: Full Plain.com feature set
- **npm Published**: Available to entire n8n community
- **Open Source**: MIT licensed, accepts community contributions

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/n8n-plain-node)*
