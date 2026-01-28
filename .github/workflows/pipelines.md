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


| Secret | Purpose |
|--------|---------|---------|
| `SERVER_IP` | VM public IP |
| `SERVER_USER` | VM SSH user |
| `SERVER_PORT` | SSH port |
| `SERVER_SSH_KEY` | **Private** SSH key |
| `DJANGO_PW` | Admin password |
| `DJANGO_EMAIL` | Admin email |
| `DJANGO_USER` | Admin username |
| `ALLOWED_HOSTS` | Django hosts |
| `SECRET_KEY` | Django secret |
| `production` | Frontend flag |
| `apiurl` | Frontend API URL |
      

Example Secret Keys are from our Environment Files. 
