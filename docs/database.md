# Database

Context QA uses **Postgres with pgvector** for the vector store and relational data. The backend connects via the URL in config (e.g. `.env`); for local development you typically use the Cloud SQL Proxy (see [Deployment](deployment.md)).

## pgvector

The init script (`app/init_db.py`) enables the pgvector extension and prepares the database. Embeddings and vector search are used for RAG in the QA and ingestion pipelines; embedding model and index settings are driven by app config (e.g. `app/config/`).

## Migrations (Alembic)

If you use Alembic in this project:

- **Naming:** Use a clear, dated slug for revisions (e.g. `2024-01-15_add_embedding_index.py`).
- **Create revision:**  
  `alembic revision --autogenerate -m "Description of change"`
- **Apply:**  
  `alembic upgrade head`

Keep migration scripts under the usual `alembic/versions` (or your chosen path) and never edit applied migrations.

## Local connection

With Cloud SQL Proxy running (see [Deployment](deployment.md)), connect with your normal Postgres client using `localhost` and the proxy port (e.g. 5432 or the one you configured).
