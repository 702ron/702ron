# AI Label Designer

> **[View full repository with screenshots and code →](https://github.com/702ron/1932-label-wizard)**

Full-stack whiskey barrel label creator powered by AI. A 4-step wizard transforms simple text input into photorealistic bottle mockups through intelligent logo generation, dynamic background creation, and real-time fine-tuning. See it live at https://labelwizard.702market.com/

## Problem
Creating professional product labels requires design expertise and significant time investment. Small distilleries and craft producers need an accessible way to generate barrel-aged label designs without hiring designers or learning complex tools.

## Solution
Built a full-stack application that orchestrates AI image generation into a seamless creative workflow. Users input barrel details → AI generates custom logos → AI creates thematic backgrounds → real-time preview with fine-tuning controls → outputs photorealistic bottle mockups. React frontend handles the interactive 4-step flow, FastAPI backend coordinates with multiple AI services, Redis caches generated assets, and MinIO stores production-ready images.

## Architecture

```
React Frontend (UI/UX)
        ↓
  FastAPI Backend
        ↓
   ┌────┴────┬─────────┬──────────┐
   ↓         ↓         ↓          ↓
 Redis   PostgreSQL  MinIO   OpenRouter/
(Cache)  (Metadata) (Storage)  Gemini
                                (AI)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React, Tailwind CSS |
| Backend | FastAPI, Python |
| AI | OpenRouter, Google Gemini |
| Caching | Redis |
| Database | PostgreSQL |
| Storage | MinIO (Object Storage) |
| Deployment | Docker, Docker Compose |

## Key Features

### Intelligent Logo Generation
AI-powered logo creation from text descriptions. The system generates custom artwork that reflects barrel age, distillery brand, and spirit type with surprising accuracy and artistic flair.

### Dynamic Background Creation
Contextual backgrounds are generated to complement the logo and overall aesthetic. Whiskey, wine, and craft spirit themes are supported with auto-scaling for label dimensions.

### Real-Time Fine-Tuning
Users control regeneration, color shifts, and composition adjustments without waiting. Preview updates instantly as parameters change, enabling quick iteration without backend delays.

### Photorealistic Mockups
Final output renders labels applied to actual product bottles, showing exact placement and visual impact. Critical for approval workflows before production.

## Results

- **Live Production**: Active at labelwizard.702market.com with live demo
- **4-Step UX**: Guided workflow reduces design decisions to 4 simple steps
- **Sub-5s Generation**: Average label generation under 5 seconds
- **API-Driven**: Fully headless API supports custom frontends and batch generation

---

*Built by [Ron](https://github.com/702ron) — [View full project →](https://github.com/702ron/1932-label-wizard)*
