# Rocket.Chat

This app runs Rocket.Chat using Docker Compose with a single-node MongoDB replica set.

## Setup

1. Copy `.env-example` to `.env` and adjust values if needed.
2. Start the stack:

   make rocketchat-up

## Notes

- The MongoDB replica set is initialized by the `rocketchat-db-init` service.
- Data is stored in the `rocketchat-db-data` volume.
