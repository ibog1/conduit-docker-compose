# CI/CD Pipeline Setup Guide
This project implements fully automated Continuous Integration & Continuous Deployment (CI/CD) pipelines using GitHub Actions.

## Table of Contents
- [Workflow](#workflow)
- [Secrets & Variables](#secrets-&-variables)

## Workflow

### 1. Create `.github/workflows/deployment.yaml`
1. Repository → **Actions** → **"New workflow"** → **"set up a workflow yourself"**
2. File name: `deployment.yaml`

### Trigger
- Automatic: Push to `main` branch
- Manual: Actions tab → **"Run workflow"**

---

## Secrets & Variables

### Repository Secrets Setup

GitHub → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

```bash
| Secret          | Purpose                    |
| `SERVER_IP`     | VM public IP address       |
| `SERVER_USER`   | SSH username on VM         |
| `SERVER_PORT`   | SSH port                   |
| `SERVER_SSH_KEY`| **Private** SSH key        |
| `DJANGO_PW`     | Django superuser password  |
| `DJANGO_EMAIL`  | Django superuser email     |
| `DJANGO_USER`   | Django superuser username  |
| `ALLOWED_HOSTS` | Django ALLOWED_HOSTS       |
| `SECRET_KEY`    | Django SECRET_KEY          |
| `production`    | Frontend production flag   |
| `apiurl`        | Frontend API base URL      |
```

> [!WARNING]
> **`SERVER_SSH_KEY` must use a private SSH key WITHOUT PASSPHRASE!**

Example Secret Keys are from our Environment Files. 
