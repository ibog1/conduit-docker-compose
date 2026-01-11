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
git clone https://github.com/ibog1/conduit-docker-compose
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
### 4. Access
```bash
Frontend: http://YOUR_VM_IP:8282
Backend API: http://YOUR_VM_IP:8000/api  
DB: localhost:5432 (Postgres persistent)
```
- On a cloud VM, open the firewall for port 8000 (backend) and 8282 (frontend).

## Usage
### Collect static files (only once per image change)
```bash
docker compose exec backend python manage.py collectstatic --noinput
```
### (Optional) Create a superuser
```bash
docker compose exec backend python manage.py createsuperuser
```
### Rebuild containers
```bash
docker compose down -v
docker compose up -d --build
```
## Logs and persistence
### Logs
```bash
  docker compose logs -f backend
  docker compose logs -f frontend
  ```
### Exec into container
```bash
docker compose exec backend bash
```
## Environment Variables
Create a ``.env`` file at the repo root. Example:
### Core
```bash
SECRET_KEY=dev-secret-only
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1,0.0.0.0
```
### CORS / CSRF: full origins (scheme + host + port)
```bash
CORS_ORIGINS=<http://localhost:4000,http://127.0.0.1:4000>
CSRF_TRUSTED_ORIGINS=<http://localhost:4000,http://127.0.0.1:4000>
```
### Static (optional; defaults used in settings.py)
```bash
STATIC_ROOT=/app/staticfiles
```
Notes
- Never commit ``.env``! Use ``.env.example`` for defaults.
- Vars: UPPER_CASE_WITH_UNDERSCORE
- Restart after changes: ``docker compose restart``
- 
