# Jenkins

This app runs Jenkins using Docker Compose.

## Setup

1. Copy `.env-example` to `.env` and adjust values if needed.
2. Start the stack:

   make jenkins-up

## First login

Jenkins uses the initial admin password flow. After the container starts, grab it with:

  docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
