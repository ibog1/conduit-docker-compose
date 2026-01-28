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
      SERVER_IP
      SERVER_PORT
      SERVER_USER
      SERVER_SSH_KEY 
      SECRET_KEY
      production
      apiurl
      DJANGO_PW 
      DJANGO_EMAIL
      DJANGO_USER 
      
```
Example Secret Keys are from our Environment Files. 
