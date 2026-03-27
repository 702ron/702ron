# Nostradamus AI — Historical Prophecy Analysis Platform

A sophisticated full-stack application for analyzing and predicting historical patterns in Nostradamus' quatrains using NLP, machine learning, and knowledge graphs. Built with FastAPI backend, React TypeScript frontend, PostgreSQL/Neo4j databases, and real-time WebSocket streaming with production Docker deployment.

## Problem

Nostradamus' prophecies contain archaic language, obscure references, and ambiguous predictions. Manual analysis is subjective and scattered across multiple sources. The challenge was building an intelligent system that processes multiple languages, extracts entities, builds knowledge relationships, and surfaces meaningful predictions with confidence scoring.

## Solution

Engineered a production-grade full-stack platform featuring:
- **NLP pipeline** with NLTK, spaCy, and TextBlob for archaic French/English processing
- **Machine learning models** using scikit-learn for pattern recognition and confidence scoring
- **Knowledge graph** (Neo4j) mapping relationships between quatrains, historical events, and figures
- **11 scraper modules** extracting prophecy data from Wikipedia, Sacred Texts, Internet Archive, and almanacs
- **Real-time WebSocket API** for live analysis streaming to frontend
- **Production deployment** via Docker, Nginx, and automated CI/CD
- **TypeScript React UI** with Redux state management and shadcn/ui components

## Architecture

```
Data Scrapers (11 modules)
    ↓
FastAPI Backend
    ├→ Auth (JWT) → Protected Routes
    ├→ NLP Pipeline (NLTK/spaCy/TextBlob)
    ├→ ML Models (scikit-learn) → Confidence Scoring
    ├→ PostgreSQL (SQLAlchemy ORM)
    └→ Neo4j (Knowledge Graph)
    ↓
WebSocket Server (real-time streaming)
    ↓
React Frontend (10 pages + GraphExplorer)
    ├→ Redux State Management
    ├→ shadcn/ui + Tailwind CSS
    └→ Vite build system
    ↓
Docker Compose → Nginx → Gunicorn → Production Deploy
```

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Backend Framework | FastAPI (Python) |
| Frontend | React, TypeScript, Vite |
| State Management | Redux |
| UI Framework | shadcn/ui, Tailwind CSS |
| Databases | PostgreSQL (SQLAlchemy), Neo4j |
| NLP | NLTK, spaCy, TextBlob |
| ML | scikit-learn, pattern recognition |
| Real-time | WebSocket (asyncio) |
| Authentication | JWT tokens |
| Deployment | Docker, Docker Compose, Nginx |
| Code Quality | 12+ test modules |

## Key Features

### Advanced NLP Processing
Custom natural language pipeline handles archaic French, extracts semantic meaning from prophecies, performs entity recognition, and normalizes historical references across multiple languages with TextBlob sentiment analysis. Pipeline includes: tokenization, lemmatization, stopword removal, and custom regex for date/number extraction from historical texts.

### Knowledge Graph Visualization
Neo4j-powered graph database maps relationships between quatrains, historical events, and key figures. GraphExplorer page provides interactive visualization of prophecy connections and event correlations with filtering, search, and export capabilities. Enables discovery of patterns humans might miss.

### ML-Driven Predictions
scikit-learn models perform feature engineering on prophecy text, apply pattern recognition algorithms, and generate confidence scores for predicted events based on historical accuracy and linguistic patterns. Uses ensemble methods combining multiple classifier types for robust predictions.

### Production-Ready Deployment
Complete Docker + Nginx + Gunicorn stack with environment configuration, health checks, and automated deployment via `deploy.sh`. Makefile simplifies development, testing, and production builds. Includes database migrations, seed data, and rollback procedures.

## Scraper Infrastructure

11 dedicated modules collect prophecy data from diverse sources:

- **Wikipedia scraper**: Historical events, key figures, timeline data
- **Sacred Texts scraper**: Full Nostradamus quatrain corpus with annotations
- **Internet Archive scraper**: Historical articles, digitized prophecy books
- **Almanac scraper**: Historical records, astronomical events, date correlations
- **News scraper**: Modern events for prediction validation
- Error handling with retry logic, rate limiting, and data deduplication

## API Endpoints

- `/auth/login` - JWT token generation
- `/quatrains/search` - Full-text search with NLP
- `/predictions/analyze` - Run ML predictions on text
- `/graph/visualize` - Neo4j relationship data
- `/events/correlate` - Match predictions to historical events
- `/ws/analysis` - WebSocket stream for real-time analysis
- `/translations/normalize` - Archaic text normalization

## Frontend Pages

- **Dashboard**: Overview of recent predictions, trending quatrains, upcoming events
- **Quatrain Browser**: Searchable prophecy database with full text, translations, annotations
- **GraphExplorer**: Interactive Neo4j visualization with filtering and drill-down
- **Predictions**: ML-driven forecast results with confidence scores and methodology
- **Events**: Historical event timeline with correlations to predictions
- **Analysis**: Detailed prophecy breakdown with NLP insights and entity extraction
- **Reports**: Export and sharing of analysis findings in PDF/JSON
- **Settings**: User preferences, language selection, theme configuration
- **Admin**: Data management, scraper control, model training interface
- **API Docs**: Interactive API explorer with live request/response examples

## Model Training Pipeline

Continuous learning from historical accuracy:

1. **Feature Engineering**: Extract linguistic patterns, date/number references, entity co-occurrence
2. **Historical Training**: Use known fulfilled prophecies as training data (supervised)
3. **Cross-Validation**: K-fold testing ensures generalization beyond training set
4. **Ensemble Methods**: Combine multiple classifier types for robust predictions
5. **Confidence Calibration**: Validate prediction confidence against actual accuracy
6. **Model Versioning**: Track performance across model iterations with A/B testing

## Results & Impact

- **83 Python modules** (scrapers, models, API handlers)
- **35 TypeScript components** with full type safety
- **10 frontend pages** plus GraphExplorer visualization
- **11 scraper modules** collecting data from diverse sources
- **Neo4j knowledge graph** with 1000+ entity relationships
- **Real-time WebSocket streaming** for live analysis results
- **Production-grade deployment** with Docker and Nginx
- **12+ test suites** ensuring reliability
- **9 documentation files** for developers and users
- **100+ API endpoints** across all services

## License

MIT

---

Built by [Ron](https://github.com/702ron)
