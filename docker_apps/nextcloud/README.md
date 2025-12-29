# Nextcloud

This app runs Nextcloud with Postgres and Redis using Docker Compose.

## Setup

1. Copy `.env-example` to `.env` and adjust values if needed.
2. Start the stack:

   make nextcloud-up

## Notes

- The database container is named `nextcloud-db`.
- Redis is used for file locking and caching.
