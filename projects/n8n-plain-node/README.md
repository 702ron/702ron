# n8n Plain.com Community Node

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white) ![n8n](https://img.shields.io/badge/n8n-FF6B35?style=flat&logo=n8n&logoColor=white) ![GraphQL](https://img.shields.io/badge/GraphQL-E10098?style=flat&logo=graphql&logoColor=white)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/n8n-plain-node)**

Open-source n8n community node for Plain.com customer support platform. GraphQL API integration covering 6 resources with full CRUD operations. Includes Plain Trigger node for real-time event subscriptions. Published to npm with TypeScript support and comprehensive documentation.

## What I Built

- **6-Resource Coverage** - Complete GraphQL integration: Customers, Conversations, Inboxes, Settings, Thread Attachments, Events
- **Full CRUD Operations** - Create, read, update, delete customers and manage all support platform features
- **Plain Trigger Node** - Real-time event subscriptions via GraphQL subscriptions without polling
- **TypeScript First** - Fully typed implementation with IDE autocomplete and compile-time safety
- **npm Published** - Installable as a community node directly in n8n; receives updates independently
- **MIT Licensed** - Open-source with contributor guidelines for community improvements
- **Comprehensive Docs** - API reference, setup instructions, and real-world usage examples
- **Production-Ready** - Tested, validated, and recommended for enterprise customer support workflows

## Architecture

```
n8n Workflow
     ↓
Plain Node Interface
  (CRUD Operations)
     ↓
GraphQL Query Builder
     ↓
Plain.com GraphQL API
     ↓
   ┌─┴──┬────────┬───────┬─────────┬──────────┬────────┐
   ↓    ↓        ↓       ↓         ↓          ↓        ↓
Customers Conversations Inboxes Settings Attachments Events
(Crud)    (Query/Get)   (Manage) (Update)  (Upload) (Trigger)
```

**Process Flow:**
1. n8n workflow node triggered (regular node) or event fires (trigger node)
2. Node translates operation to GraphQL query/mutation
3. Sends authenticated request to Plain.com API
4. API processes and returns structured JSON response
5. n8n passes data to next workflow step
6. For triggers: subscriptions receive real-time events and execute workflow

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Framework** | n8n Community Nodes SDK | Node development and lifecycle |
| **Language** | TypeScript | Type-safe implementation, IDE support |
| **API Protocol** | GraphQL | Query language for Plain.com API |
| **Authentication** | API Key | Plain.com credential management |
| **Package Manager** | npm | Distribution and version management |
| **Testing** | Jest | Unit and integration test coverage |
| **Documentation** | Markdown + JSDoc | API reference and examples |

## Key Features

### 6-Resource Complete Coverage
Comprehensive GraphQL coverage of Plain.com: create/read/update customers, query conversations, manage inboxes, update settings, attach files to threads, and subscribe to real-time customer messaging events.

### Trigger Node for Real-Time Events
Plain Trigger node subscribes to GraphQL subscriptions for customer messaging events. Enables automation workflows triggered by incoming messages, customer status changes, or conversation updates without polling.

### TypeScript First
Fully typed implementation ensures IDE autocomplete, compile-time safety, and reduced integration bugs. Developers see available fields and operations immediately during workflow building.

### Published to npm
Installable as a community node directly in n8n with `npm install n8n-nodes-plain`. Receives updates independently of n8n core releases and integrates seamlessly with existing workflows.

## Setup

Installation via n8n, API credentials, resource documentation, real-world workflow examples, and contribution guidelines are available in the [full repository](https://github.com/702ron/n8n-plain-node).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/n8n-plain-node)*
