# Getting Started

## Prerequisites

- Python 3.x
- [Poetry](https://python-poetry.org/)
- Access to the database (Cloud SQL Proxy for local dev; see [Deployment](../deployment.md))

## Backend setup

From the repo root:

```bash
cd backend
poetry install
poetry shell
```

Ensure a `.env` file exists (e.g. copy from `.env.example`) with database URL, secrets, and any API keys used by the app.

## Database

1. Start Cloud SQL Proxy (see [Deployment](../deployment.md)).
2. Run init script to enable pgvector and create the superuser:

   ```bash
   python app/init_db.py
   ```

## Data ingestion

Put PDFs in `data/raw` and run:

```bash
python app/ingestion/run.py
```

Config for ingestion and chat is under `app/config/` (e.g. `ingestion.yml`, `chat.yml`).

## Running the API locally

From `backend` with the virtualenv active:

```bash
uvicorn app.main:app --reload
```

API docs: `http://localhost:8000/api/v1/docs` (or the port you use).

## Frontend integration

Use the login endpoint to get an access token, then call the QA chat endpoint with:

- `Authorization: Bearer <token>`
- `Content-Type: application/json`
- Body: `{ "message": "Your question" }`

See the main [README](../../README.md) for a minimal Next.js fetch example.
