# DevOps Internship Assignment: Django Deployment

Welcome to your practical assessment. You have been provided with a working Django Rest Framework (DRF) application. Your goal is to containerize this application, set up a CI/CD pipeline, and deploy it to a cloud provider.

## Project Overview

The project is a simple API with a single endpoint `/api/hello/` that returns a message from the database.
-   **Core**: Django 5.x
-   **Database**: SQLite (for simplicity, you may switch to PostgreSQL if you wish, but it's not required).
-   **Environment**: Uses `python-dotenv` for configuration.

### Local Setup (for your reference)
1.  `python -m venv venv`
2.  `.\venv\Scripts\Activate` (Windows) or `source venv/bin/activate` (Mac/Linux)
3.  `pip install -r requirements.txt`
4.  Create a `.env` file based on your needed configuration (see `settings.py`).
5.  `python manage.py migrate`
6.  `python manage.py runserver`

---

## Your Tasks

### Task 1: Containerization (Docker)
1.  Create a `Dockerfile` for the Django application.
    -   Use a lightweight Python image (e.g., `python:3.11-slim`).
    -   Use **Gunicorn** as the production application server (you may need to add it to `requirements.txt`).
    -   Ensure static files are collected during the build or startup process.
2.  Create a `docker-compose.yml` file to orchestrate the services locally.
    -   Define the Django application service.
    -   Define an **Nginx** service (see Task 2).

### Task 2: Web Server (Nginx)
1.  Configure Nginx as a reverse proxy.
    -   It should forward traffic to the Gunicorn/Django container.
    -   It should serve **static files** directly (Django should not serve static files in production).
2.  Ensure standard security headers are set.

### Task 3: CI/CD Pipeline (GitHub Actions)
1.  Create a GitHub Actions workflow (`.github/workflows/deploy.yml`).
2.  The pipeline should:
    -   Lint the code (e.g., using `flake8`).
    -   Run tests (use `python manage.py test`).
    -   Build the Docker image.

### Task 4: Deployment (Render)
1.  Deploy the application to **Render** (render.com).
    -   You can use Render's "Web Service" with the Docker runtime.
2.  **Configuration**:
    -   Ensure environment variables (`SECRET_KEY`, `DEBUG`) are set in Render's dashboard, NOT hardcoded in the image.
    -   Ensure the database persists (or use Render's managed PostgreSQL if you prefer).
3.  **Submission**:
    -   The live URL (e.g., `https://your-app.onrender.com/api/hello/`) should return a successful response.

## Deliverables
-   A GitHub repository link with your code (Dockerfile, Nginx config, CI/CD workflow).
-   The live URL of the deployed application.
-   A brief text file or markdown document explaining your approach.

Good luck!


---------------------------------------------------------------------------------------------------------------------------------------------------------

# DevOps Internship Assignment – Django Deployment

This repository contains my solution for the DevOps Internship Assignment.  
The task involved containerizing a Django REST application, setting up a CI pipeline, and deploying it to a cloud platform.

---

## Overview

The application is a simple Django REST API with one endpoint:

```

/api/hello/

```

It returns a message stored in the database.

The focus of this assignment was not application development, but **deployment, CI/CD, and environment configuration**.

---

## Changes Made & Files Created

### 1. Dockerization

**Files created/updated:**
- `Dockerfile`
- `docker-compose.yml`

**What I did:**
- Created a Dockerfile using `python:3.11-slim`
- Installed dependencies from `requirements.txt`
- Used Gunicorn as the production server
- Collected static files during the build
- Used Docker Compose to run Django and Nginx together locally

---

### 2. Nginx Reverse Proxy

**Files created:**
- `nginx/nginx.conf`

**What I did:**
- Configured Nginx as a reverse proxy
- Forwarded requests to the Django app running on Gunicorn
- Served static files through Nginx instead of Django

---

### 3. Environment Configuration

**Files involved:**
- `.env` (local only)
- Render environment variables

**What I did:**
- Used environment variables for `SECRET_KEY`, `DEBUG`, and `ALLOWED_HOSTS`
- Ensured secrets are NOT hardcoded in the image
- Added a fallback `SECRET_KEY` in `settings.py` only for CI test execution

---

### 4. CI/CD Pipeline (GitHub Actions)

**Files created:**
- `.github/workflows/deploy.yml`

**Pipeline steps:**
- Checkout code
- Set up Python 3.11
- Install dependencies
- Run `flake8` for linting
- Run Django tests
- Build Docker image

**Fixes applied:**
- Installed flake8 explicitly in CI
- Adjusted linting rules to avoid non-critical failures
- Fixed test failures caused by missing environment variables

---

### 5. Cloud Deployment (Render)

**What I did:**
- Deployed the app using Render’s Docker runtime
- Set the start command using Gunicorn
- Configured environment variables in Render dashboard
- Verified deployment using the live API endpoint

**Live URL:**
```

[https://devops-intern-task-1-jp0v.onrender.com/api/hello/](https://devops-intern-task-1-jp0v.onrender.com/api/hello/)

```
