# n8n

This app runs n8n with a Postgres database using Docker Compose.

## Setup

1. Copy `.env-example` to `.env` and fill in values.
2. Start the stack:

   make n8n-up

## Notes

- The database container is named `n8n-db`.
- Persisted data is stored in Docker volumes: `n8n-data` and `n8n-postgres-data`.
