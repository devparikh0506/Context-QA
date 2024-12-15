# Project Structure

Context QA is organized as a monorepo with backend, docs, and (when present) frontend/infra in separate areas.

## Repository layout

```
Context QA/
├── backend/           # FastAPI + LangChain app
│   ├── app/
│   │   ├── api/       # Routes, deps
│   │   ├── config/    # YAML config (chat, ingestion)
│   │   ├── core/      # Config, db, security
│   │   ├── crud/      # User CRUD
│   │   ├── ingestion/ # RAG ingestion pipeline
│   │   ├── models/    # SQLAlchemy models
│   │   ├── schemas/   # Pydantic schemas
│   │   ├── utils/
│   │   ├── init_db.py
│   │   └── main.py    # App entrypoint
│   ├── Dockerfile
│   ├── pyproject.toml
│   └── poetry.lock
├── docs/              # Project documentation
├── cloudbuild.yaml    # CI/CD
└── README.md
```

## Backend (`backend/app`)

| Area | Purpose |
|------|--------|
| `api/` | FastAPI routers (`login`, `qa`), dependency injection |
| `config/` | Chat and ingestion settings (YAML) |
| `core/` | App config, DB connection, security (e.g. JWT) |
| `crud/` | Database operations (e.g. user_crud) |
| `ingestion/` | Document ingestion and embedding pipeline |
| `models/` | SQLAlchemy models (e.g. user) |
| `schemas/` | Request/response schemas (chat, ingestion) |
| `init_db.py` | One-time DB setup (pgvector, superuser) |

API versioning is under `/api/v1/` (e.g. `/api/v1/qa/chat`, `/api/v1/login/access-token`).
