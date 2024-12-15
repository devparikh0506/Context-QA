# Context QA Documentation

**Author:** Dev Parikh

Context QA is a RAG-based question-answering system backed by a vector database (Postgres with pgvector), with a FastAPI backend and LangChain for retrieval-augmented generation. The backend is deployed on Google Cloud Run with Cloud SQL and Redis; the frontend targets Next.js on Vercel, with optional usage limits via Stripe subscriptions.

## Overview

- **Backend:** FastAPI, LangChain, pgvector (Postgres)
- **Frontend:** Next.js (Vercel)
- **Infrastructure:** Terraform (Cloud Run, Cloud SQL, Redis), Cloud Build
- **Billing:** Stripe for subscription-based usage

## Documentation

| Section | Description |
|--------|-------------|
| [Getting started](getting-started/installation.md) | Environment setup, Poetry, database init, ingestion |
| [Project structure](project-structure.md) | Repository layout and main components |
| [Database](database.md) | pgvector, migrations, and schema practices |
| [Deployment](deployment.md) | GCP, Terraform, Cloud SQL, Cloud Build |
| [Changelog](changelog.md) | Release history and notable changes |

## Quick links

- **API docs (live):** `https://<your-cloud-run-url>/api/v1/docs`
- **Login/token:** `POST /api/v1/login/access-token`
- **Chat/QA:** `POST /api/v1/qa/chat`

Maintained by **Dev Parikh**. Contributions welcome.
