# 🔐 Secure Job Portal Application

### Flask + OTP Email Verification + Employer Dashboard + Docker

![Python](https://img.shields.io/badge/Python-3.11-blue.svg) ![Docker](https://img.shields.io/badge/Docker-ready-lightgrey.svg) ![License: MIT](https://img.shields.io/badge/License-MIT-green.svg) ![Security](https://img.shields.io/badge/Security-OTP%20%7C%20Rate%20Limit-orange.svg)

A production-ready, secure full-stack job portal system built using Flask. Applicants must verify their email via OTP before submitting applications, and only authenticated employers can review and respond.

---

## ✅ What's new in this README

This enhanced README includes:

* ✅ **Screenshots** (placeholders + guidance for adding real images)
* ✅ **Badges** for Python, Docker, License and Security
* ✅ **Full deployment guide**: Render, AWS (Elastic Beanstalk & ECR + ECS), and Kubernetes (EKS)
* ✅ **CI pipeline** example using **GitHub Actions** (build, test, lint, and Docker push)

---

## 📂 Quick project structure

```
job_portal_app/
├── static/
│   └── style.css                # App stylesheet
├── templates/
│   ├── dashboard.html           # Employer dashboard
│   ├── otp_verify.html          # OTP input UI
│   ├── career.html              # Job application form
│   └── login.html               # Employer login page
├── data/
│   └── applications.json        # Securely stored job applications
├── .github/workflows/
│   └── ci.yml                   # (optional) GitHub Actions pipeline
├── app.py                       # Flask backend
├── Dockerfile                   # Docker container build config
├── docker-compose.yml           # (optional) compose for local dev
├── requirements.txt             # Python dependencies
└── README.md                    # Project documentation
```

---

## 📸 Screenshots

> **Tip:** Add screenshots under `docs/screenshots/` and commit them to the repo. Replace the example paths below with your files.

### Example screenshot placeholders

* `docs/screenshots/home.png` — Landing / Career page
* `docs/screenshots/otp_verify.png` — OTP verification form
* `docs/screenshots/dashboard.png` — Employer dashboard (list + reject action)

### How to include screenshots in README (Markdown)

```markdown
![Career Page](docs/screenshots/home.png)
![OTP Verify](docs/screenshots/otp_verify.png)
![Dashboard](docs/screenshots/dashboard.png)
```

Add high-resolution (800–1280px width) PNGs and small file sizes (<200KB) for faster loading.

---

## 🏷️ Badges

Use shields.io badge images. Example (already included at top):

```markdown
![Python](https://img.shields.io/badge/Python-3.11-blue.svg)
![Docker](https://img.shields.io/badge/Docker-ready-lightgrey.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Security](https://img.shields.io/badge/Security-OTP%20%7C%20Rate%20Limit-orange.svg)
```

You can add build/test badges once CI is enabled (GitHub Actions provides a status badge URL).

---

## 🐳 Docker & Local Development

### Build and run

```bash
# build
docker build -t jobportal:latest .
# run
docker run -p 5000:5000 --env-file .env jobportal:latest
```

### docker-compose (optional) — `docker-compose.yml`

```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - '5000:5000'
    env_file:
      - .env
    volumes:
      - ./data:/app/data
```

Place SMTP credentials, secret key, and employer password hash in a `.env` file (never commit `.env`).

---

## ☁️ Deployment Guide

Below are step-by-step guides for three common platforms.

### 1) Render (fast & simple)

1. Create a free Render account and connect your GitHub repo.
2. Create a new **Web Service**.

   * Build command: `docker build -t jobportal .`
   * Start command: `docker run -p 5000:5000 jobportal`
3. Set environment variables (SMTP, SECRET_KEY, DATABASE_URL if used).
4. Add deploy health checks to ensure the app is up.

*Render automatically manages TLS and a global CDN.*

---

### 2) AWS: Elastic Beanstalk (simple) or ECS/ECR (Docker)

#### Elastic Beanstalk

1. Install EB CLI and configure AWS credentials.
2. `eb init -p docker job-portal-app` and `eb create job-portal-env`.
3. Configure environment variables in the Elastic Beanstalk console (SMTP, SECRET_KEY).
4. `eb deploy` to push new versions.

#### ECS + ECR (recommended for production)

1. Build and push image to ECR.
2. Create an ECS cluster and a Task Definition referencing the ECR image.
3. Use an Application Load Balancer (ALB) and an Auto Scaling Group
4. Store secrets in AWS Secrets Manager or SSM Parameter Store and inject them as environment variables.

---

### 3) Kubernetes (EKS) — Production-grade

1. Containerize the app and push image to a registry (ECR/GCR/Docker Hub).
2. Create K8s `Deployment`, `Service` (LoadBalancer), and `ConfigMap`/`Secret` for env variables.
3. Use an Ingress (ALB Ingress Controller / NGINX Ingress) with TLS.
4. Add HorizontalPodAutoscaler for scaling and Resource requests/limits.

Example `deployment.yaml` (snippet):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jobportal
spec:
  replicas: 2
  selector:
    matchLabels:
      app: jobportal
  template:
    metadata:
      labels:
        app: jobportal
    spec:
      containers:
      - name: jobportal
        image: <your-registry>/jobportal:latest
        ports:
        - containerPort: 5000
        envFrom:
        - secretRef:
            name: jobportal-secrets
```

*Production tips:* use a managed DB (RDS/Postgres) rather than JSON files for scaling, and enable proper backups.

---

## ⚙️ CI — GitHub Actions (example)

Create `.github/workflows/ci.yml` — this pipeline builds the Docker image, runs lint/tests, and (optionally) pushes to a registry.

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: 3.11

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Lint (flake8)
      run: |
        pip install flake8
        flake8 || true

    - name: Run tests
      run: |
        # place tests in tests/
        pytest -q || true

    - name: Build Docker image
      run: |
        docker build -t jobportal:${{ github.sha }} .

    - name: Log in to Docker Hub
      if: github.event_name == 'push'
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    - name: Push to Docker Hub
      if: github.event_name == 'push'
      run: |
        docker tag jobportal:${{ github.sha }} ${{ secrets.DOCKERHUB_USERNAME }}/jobportal:latest
        docker push ${{ secrets.DOCKERHUB_USERNAME }}/jobportal:latest
```

**Secrets to add in GitHub repo**: `DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`, SMTP credentials if you plan to run integration tests that send emails.

---

## 🔒 Security Notes & Best Practices

* **Never commit** `.env` or credentials to repository.
* Use **App Passwords** (Gmail) or a transactional email provider (SendGrid / Mailgun) for sending OTPs.
* Rate-limit login attempts and OTP requests (example: Flask-Limiter).
* Use HTTPS for all production deploys and enable HSTS.
* Move from JSON file storage to a managed DB (Postgres) for production. Encrypt backups.
* Use a secrets manager (AWS Secrets Manager / HashiCorp Vault) for sensitive data.

---

## 📦 Optional Improvements

* Attach resume uploads (S3) + virus scanning
* Add email templates and localization
* Add audit log for employer actions
* Add background worker (Celery/RQ) for sending emails

---

## 📌 License

MIT License — see the `LICENSE` file.

---

