# conduit-docker-compose
Dockerized Conduit (RealWorld API spec) with Angular frontend, Django REST backend, PostgreSQL DB. Production-ready with nginx proxy, Gunicorn, multi-stage builds.

---

## Table of Contents
- [Project Description](#project-description)
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Environment Variables](#environment-variables)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)

---

## Project Description
Fullstack Conduit app following RealWorld API spec. Features JWT auth, articles CRUD, profiles/follow, tags/favorites, feeds. Deployed on VM via Docker Compose (3 services). **Security hardened**: Secrets/IPs removed from code → .env only (.gitignore). Accessible via nginx proxy on port 8282.

---

## Quickstart

### Prerequisites
- Docker & Docker Compose
- Git
