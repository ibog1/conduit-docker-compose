# conduit-docker-compose
Fullstack Conduit app following RealWorld API spec. Features JWT auth, articles CRUD, profiles/follow, tags/favorites, feeds. Deployed on VM via Docker Compose (3 services). **Security hardened**: Secrets/IPs removed from code → .env only (.gitignore). Accessible via nginx proxy on port 8282.

---

## Table of Contents
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Environment Variables](#environment-variables)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)

---

## Quickstart

### Prerequisites
- Docker & Docker Compose
- Git
### 1. Clone the repo 
```bash
git clone 
cd conduit-backend
```
### 2. Create a .env file (see template below)
```bash
cp .env.example .env
```
> [!NOTE]  
> adjust values as needed
### 3. Build and start
Local development (host ports: backend 8000):
```bash
docker compose up -d --build
```
