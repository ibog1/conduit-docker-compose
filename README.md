# conduit-docker-compose
Fullstack Conduit app following RealWorld API spec. Features JWT auth, articles CRUD, profiles/follow, tags/favorites, feeds. Deployed on VM via Docker Compose (3 services). **Security hardened**: Secrets/IPs removed from code → .env only (.gitignore). Accessible via nginx proxy on port 8282.

---

## Table of Contents
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)

---

## Quickstart

### Prerequisites

| Tool            | Version Recommendation | Purpose                              |
|-----------------|------------------------|--------------------------------------|
| [Git]         | ≥ 2.30                 | Clone the repository                 |
| [Docker]     | ≥ 24.0                 | Container runtime                    |

---

### 1. Clone the repo 
```bash
git clone https://github.com/ibog1/conduit-docker-compose
```
### 2. Navigate to the Correct Direcotry: 
```bash
cd conduit-fullstack
```

### 3. Clone all Submodules 
```bash
git submodule update --init --recursive
```

### 4. Copy your Backend Environement file.
Naviagte: 
```bash
cd backend
```

Copy the File: 
```bash
cp example.env .env
```
> [!NOTE]  
> adjust values as needed

Navigate Back to Root: 
```bash
cd ..
```

### 5. Build and start Docker Compose 
```bash
docker compose up --build
```

### 6. Access
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
---

> [!IMPORTANT]
> Never commit ``.env``! Use ``.env.example`` for defaults.

---

> [!NOTE]
> Vars: UPPER_CASE_WITH_UNDERSCORE and restart after changes: ``docker compose restart``
