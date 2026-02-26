# EasyRAG Docker Deployment

This repository contains the production Docker Compose setup for EasyRAG.

Website: https://easyrag.cloud

## Quick start

1. Copy the example environment file:

```bash
cp .env.example .env
```

2. Edit `.env` and fill in the required values.

3. Start the stack:

```bash
docker compose -f docker-compose.prod.yml up -d
```

The web app will be available at:
- http://localhost:7771

The API will be available at:
- http://localhost:7772

## Environment variables

### Backend database
- `NODE_ENV`: Runtime environment (default `test`).
- `DATABASE_HOST`: Postgres host for the main EasyRAG database.
- `DATABASE_PORT`: Postgres port for the main EasyRAG database.
- `DATABASE_USER`: Postgres user for the main EasyRAG database.
- `DATABASE_PASSWORD`: Postgres password for the main EasyRAG database.
- `DATABASE_NAME`: Postgres database name for EasyRAG.

### MCP vector database (optional MCP server)
- `MCP_DB_USER`: Postgres user for the MCP vector database.
- `MCP_DB_PASSWORD`: Postgres password for the MCP vector database.
- `MCP_DB_NAME`: Postgres database name for the MCP vector database.

### JWT and security
- `JWT_SECRET`: JWT signing secret for access tokens (min 32 chars).
- `JWT_REFRESH_SECRET`: JWT signing secret for refresh tokens (min 32 chars).
- `JWT_EXPIRES_IN`: Access token lifetime (default `15m`).
- `JWT_REFRESH_EXPIRES_IN`: Refresh token lifetime (default `7d`).
- `ENCRYPTION_KEY`: Base64 32-byte encryption key for stored credentials.

### Frontend
- `CLIENT_ORIGIN`: Public URL of the web app used for CORS.

### LLM / embeddings
- `INTERNAL_LLM_PROVIDER`: Internal provider used by rag-service (`openai` or `mistral`).
- `INTERNAL_LLM_API_KEY`: API key for the selected `INTERNAL_LLM_PROVIDER`.
- `INTERNAL_EMBEDDING_MODEL`: Optional embedding model override.
- `SYSTEM_PROMPT_MODEL`: Optional prompt-generation model override.
- `OPENAI_API_KEY`: Optional fallback for backward compatibility when `INTERNAL_LLM_API_KEY` is not set.

### Public shared LLM credential (optional)
- `PUBLIC_LLM_API_KEY`: API key exposed as a shared credential for all users.
- `PUBLIC_LLM_PROVIDER`: Provider for the shared credential (`openai`, `mistral`).
- `PUBLIC_LLM_NAME`: Display name for the shared credential.
- `PUBLIC_LLM_DAILY_MESSAGE_LIMIT`: Per-user daily cap when using the shared credential.

### LLM service vector database
- `PGVECTOR_USER`: Postgres user for the LLM vector database.
- `PGVECTOR_PASSWORD`: Postgres password for the LLM vector database.
- `PGVECTOR_HOST`: Hostname for the LLM vector database.
- `PGVECTOR_PORT`: Port for the LLM vector database.
- `PGVECTOR_DATABASE`: Database name for the LLM vector database.

### Email verification (optional)
- `EMAIL_VERIFICATION_TTL_MIN`: Verification token time-to-live (minutes).

### SMTP (optional)
- `SMTP_HOST`: SMTP server host.
- `SMTP_TLS_REJECT_UNAUTHORIZED`: Disable TLS verification (`false` or `true`).
- `SMTP_PORT`: SMTP server port.
- `SMTP_SECURE`: Use SSL/TLS (`true` or `false`).
- `SMTP_USER`: SMTP username.
- `SMTP_PASS`: SMTP password.
- `EMAIL_FROM`: Default sender address.

## Plans and functionality

EasyRAG supports multiple plans. The active plan is validated by the license system.

- **Free**
  - Basic chatbots
  - Core document ingestion
  - Limited daily usage

- **Registered**
  - Higher daily limits
  - Monitoring and analytics

- **Pro**
  - Advanced usage limits
  - Monitoring and analytics
  - MCP servers and extended integrations

Contact us for the latest plan details and onboarding guidance.

## Notes

- For production deployments, set strong secrets and use a reverse proxy for TLS.
