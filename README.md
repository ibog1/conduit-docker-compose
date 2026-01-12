# Conduit Docker Compose
Fullstack Conduit app following RealWorld API spec. Features JWT auth, articles CRUD, profiles/follow, tags/favorites, feeds. Deployed on VM via Docker Compose (3 services). **Security hardened**: Secrets/IPs removed from code → .env only (.gitignore). Accessible via nginx proxy on port 8282.

---

## Table of Contents
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Project Structure](#project-structure)

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
cd conduit-docker-compose
```

### 3. Clone all Submodules 
```bash
git submodule update --init --recursive
```

### 4. Copy your Backend Environement file.
Naviagte: 
```bash
cd conduit-backend
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

### Collect static files
Collect CSS/images for Django Admin once per image change.
```bash
docker compose exec backend python manage.py collectstatic --noinput
```

### Create a superuser (Optional) 
Create Django admin user for `/admin` access.
```bash
docker compose exec backend python manage.py createsuperuser
```

### Rebuild containers after config changes
Full rebuild required after `.env` modifications.
```bash
docker compose down -v
docker compose up -d --build
```

### Logs
Monitor backend/frontend logs for debugging.
```bash
docker compose logs -f backend
docker compose logs -f frontend
```

### Access container shell
Execute commands directly inside containers
```bash
docker compose exec backend bash
docker compose exec frontend sh
```

### Clear frontend cache (stale assets)
Remove cached Angular/nginx files if frontend appears outdated.
 ```bash
 docker compose exec frontend rm -rf /usr/share/nginx/html/*
 docker compose up -d --build frontend
 ```

### Configuration customization
 Modify VM IP, passwords, or production settings in `.env`:  
   - `DJANGO_ALLOWED_HOSTS=*,new-vm-ip,localhost`  
   - `POSTGRES_PASSWORD=strong-password`  
   - `DEBUG=False` (production)
   - Restart: `docker compose restart`

### Environment Variables (.env.example)
**Core**
```bash
DJANGO_ALLOWED_HOSTS=*,localhost,your-vm-ip
SECRET_KEY=generate-with-django-command
DEBUG=True
```

**DB/CORS:**
```bash
POSTGRES_PASSWORD=strongpass
CORS_ORIGINS=http://localhost:8282,http://your-vm-ip:8282
```

---

> [!IMPORTANT]
> Never commit ``.env``! Use ``.env.example`` for defaults.

---

> [!NOTE]
> Vars: UPPER_CASE_WITH_UNDERSCORE and restart after changes: ``docker compose restart``

---

## Project Structure

```bash
conduit-docker-compose/                     # MAIN REPOSITORY (docker-compose orchestrates everything)
│
├── docker-compose.yaml                     # Control center (3 services, ports 8282 / 8000 / 5432)
├── .env.example                            # Public environment template (safe for Git)
├── .env                                    # Secret environment variables (passwords, IPs, gitignored)
├── .gitignore                              # Protects .env and other sensitive files
├── .dockerignore                           # Docker build optimization
│
├── conduit-backend/                        # Django backend submodule (build: ./conduit-backend)
│   ├── Dockerfile                          # Multi-stage build, Gunicorn on port 5000
│   ├── conduit/
│   │   ├── settings.py                     # Uses os.environ.get('SECRET_KEY')
│   │   └── apps/                           # Articles, Auth, Profiles apps
│   └── requirements.txt                    # Django, DRF, psycopg2
│
├── conduit-frontend/                       # Frontend submodule (Angular, build: ./conduit-frontend)
│   ├── Dockerfile                          # Multi-stage build, nginx on port 80
│   ├── nginx.conf                          # proxy_pass /api → backend:5000
│   └── src/
│       ├── environments/
│       │   └── environment.ts              # apiUrl: '/api' (via reverse proxy)
│       └── app/
│           └── core/
│               └── interceptors/           # Automatically prefixes API calls with /api
│
└── volumes / networks                      # postgres_data (persistent volume), conduit-net (Docker network)
```

