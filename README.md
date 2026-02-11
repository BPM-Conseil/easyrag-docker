# EasyRAG Docker Deployment

This repository contains the production Docker Compose setup for EasyRAG.

Website: https://easyrag.world (coming soon)

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
- `OPENAI_API_KEY`: OpenAI API key for embeddings.

### LLM service vector database
- `PGVECTOR_USER`: Postgres user for the LLM vector database.
- `PGVECTOR_PASSWORD`: Postgres password for the LLM vector database.
- `PGVECTOR_HOST`: Hostname for the LLM vector database.
- `PGVECTOR_PORT`: Port for the LLM vector database.
- `PGVECTOR_DATABASE`: Database name for the LLM vector database.

### License
- `LICENSE_PUBLIC_KEY`: Base64 Ed25519 public key to validate licenses.
- `LICENSE_KEY`: Optional license key value.
- `LICENSE_FILE_PATH`: Path to license file (default `/data/license.key`).
- `LICENSE_VALIDATION_URL`: License validation service URL.
- `LICENSE_SERVICE_URL`: License service URL for admin operations.
- `LICENSE_VALIDATION_INTERVAL_HOURS`: Hours between validation checks.
- `LICENSE_OFFLINE_GRACE_DAYS`: Days allowed offline before downgrade to Free.

### Internal service auth
- `NODE_INTERNAL_TOKEN_PRIVATE_KEY`: Base64 Ed25519 private key for internal tokens.
- `INTERNAL_TOKEN_PUBLIC_KEY`: Base64 Ed25519 public key for internal tokens.

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

- The MCP service block is commented out by default. Uncomment it if you plan to run MCP servers.
- For production deployments, set strong secrets and use a reverse proxy for TLS.
