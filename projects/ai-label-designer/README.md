# AI Label Designer

![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white) ![OpenRouter](https://img.shields.io/badge/OpenRouter-FF6B35?style=flat&logoColor=white) ![Google%20Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?style=flat&logo=google&logoColor=white)

> **[View full repository with screenshots and code &rarr;](https://github.com/702ron/1932-label-wizard)**

Full-stack whiskey barrel label creator powered by AI. A 4-step wizard transforms simple text input into photorealistic bottle mockups through intelligent logo generation, dynamic background creation, and real-time fine-tuning. **[See it live &rarr;](https://labelwizard.702market.com/)**

## What I Built

- **4-Step Guided Wizard** - Reduces complex design decisions to simple inputs: barrel details → logo concepts → background themes → final mockup
- **AI Logo Generation** - OpenRouter/Gemini creates custom brand-specific logos reflecting spirit type, aging details, and distillery style
- **Dynamic Backgrounds** - Contextual AI-generated backdrops complement logos with whiskey/wine/craft spirit aesthetics
- **Real-Time Preview** - Instant regeneration and parameter adjustments without backend delays
- **Photorealistic Mockups** - Final output shows labels applied to actual product bottles for approval workflows
- **Sub-5s Generation** - Optimized with Redis caching and intelligent request batching
- **Production Storage** - MinIO object storage for scalable image handling

## Architecture

```
User Input (4-Step Form)
         ↓
   React Frontend
         ↓
   FastAPI Coordinator
         ↓
    ┌────┴────┬─────────┬──────────┐
    ↓         ↓         ↓          ↓
  Redis   PostgreSQL  MinIO   OpenRouter/
 (Cache)  (Metadata) (Storage)  Gemini
                                (AI)
```

**Process Flow:**
1. User enters barrel/spirit details in React form
2. FastAPI validates and checks Redis cache
3. Cache miss → calls OpenRouter for logo, Gemini for background
4. Generated images stored in MinIO
5. Metadata recorded in PostgreSQL
6. React renders photorealistic mockup
7. User refines or exports final label

## Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Frontend** | React, Tailwind CSS | Interactive 4-step UI with real-time preview |
| **Backend** | FastAPI, Python | Orchestrates AI services, coordinates workflows |
| **AI Services** | OpenRouter, Google Gemini | Logo and background generation |
| **Caching** | Redis | Instant regeneration, reduce AI calls |
| **Database** | PostgreSQL | Metadata, user sessions, audit trail |
| **Storage** | MinIO | Scalable image storage, object serving |
| **Deployment** | Docker Compose | Full-stack local + cloud deployment |

## Key Features

### Intelligent Logo Generation
AI-powered logo creation directly from text descriptions. The system generates custom artwork that reflects barrel age, distillery brand, and spirit type with surprising accuracy and artistic flair. No design background required.

### Dynamic Background Creation
Contextual backgrounds are generated to complement the logo and overall aesthetic. Supports whiskey, wine, and craft spirit themes with auto-scaling for perfect label dimensions.

### Real-Time Fine-Tuning
Users control regeneration, color shifts, and composition adjustments without waiting. Preview updates instantly as parameters change, enabling quick iteration cycles without backend bottlenecks.

### Photorealistic Mockups
Final output renders labels applied to actual product bottles, showing exact placement, lighting, and visual impact. Critical for approval workflows before sending to print production.

## Setup

Detailed setup instructions, environment variables, Docker configuration, and API examples are available in the [full repository](https://github.com/702ron/1932-label-wizard).

## License

MIT

---

*Built by [Ron](https://github.com/702ron) — [View full project with screenshots &rarr;](https://github.com/702ron/1932-label-wizard)*
