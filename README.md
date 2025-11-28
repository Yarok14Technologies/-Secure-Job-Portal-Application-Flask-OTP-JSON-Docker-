
---

## 🛡️ Secure Job Portal Application

### Flask + OTP Email Verification + Employer Dashboard + Docker + CI/CD

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.3+-green.svg)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)
![Security](https://img.shields.io/badge/Security-Enhanced-red.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![CI](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-brightgreen.svg)

---

A secure full-stack job application portal built using **Flask**, featuring:

✔ OTP-secured email verification
✔ Employer-only secure dashboard
✔ JSON-based application storage
✔ Rejection email automation
✔ Flask-Login & session protection
✔ Rate limiting against brute-force attacks
✔ Full Docker support
✔ GitHub Actions CI pipeline

---

## 📌 Screenshots

> 📸 List of actual screenshots will be added soon.

| Login                           | OTP Verify                    | Employer Dashboard                  |
| ------------------------------- | ----------------------------- | ----------------------------------- |
| ![](docs/screenshots/login.png) | ![](docs/screenshots/otp.png) | ![](docs/screenshots/dashboard.png) |

---

## 📂 Project Structure

```bash
job_portal_app/
├── app.py
├── config.py
├── database.py
├── utils/
│   ├── email_service.py
│   ├── otp_manager.py
│   └── rate_limiter.py
├── routes/
│   ├── auth_routes.py
│   ├── employer_routes.py
│   └── applicant_routes.py
├── models/
│   ├── user.py
│   └── application.py
├── templates/
│   ├── base.html
│   ├── login.html
│   ├── otp_verify.html
│   ├── dashboard.html
│   └── career.html
├── static/
│   ├── style.css
│   └── logo.png
├── data/
│   └── applications.json
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .env.example
├── LICENSE
├── CONTRIBUTING.md
├── README.md
├── .github/
│   └── workflows/
│       └── ci.yml
└── docs/
    ├── deployment.md
    └── screenshots/
        ├── login.png
        ├── otp.png
        └── dashboard.png
```

---

## 🛠 Installation Guide

### Local Setup

```sh
git clone https://github.com/yourname/job_portal_app.git
cd job_portal_app
pip install -r requirements.txt
python app.py
```

Visit:
👉 `http://localhost:5000`

---

## 🐳 Docker Deployment

### Build Image

```sh
docker build -t jobportal .
```

### Run Container

```sh
docker run -p 5000:5000 jobportal
```

Or using Docker Compose:

```sh
docker-compose up --build
```

---

## 📧 SMTP Email Configuration

Update `.env`:

```env
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
SMTP_EMAIL=your-email@gmail.com
SMTP_PASSWORD=your-app-password
```

To use Gmail securely:
[https://support.google.com/accounts/answer/185833](https://support.google.com/accounts/answer/185833)

---

## 🔐 Employer Login Credentials (Dev Mode)

| Email                                               | Password       |
| --------------------------------------------------- | -------------- |
| [employer@example.com](mailto:employer@example.com) | securepassword |

⚠️ Recommendation: Change in production immediately!

---

## 🚀 Deployment

Full docs available here:
📄 `docs/deployment.md`

Supported Cloud Platforms:

| Platform          |       Status       |
| ----------------- | :----------------: |
| Render.com        | ✔️ Free deployment |
| AWS ECS (Fargate) |     ✔️ Scalable    |
| Kubernetes        |  ✔️ Industry-grade |

---

## 🔁 CI/CD — GitHub Actions

Workflow file:
`.github/workflows/ci.yml`

✔ Auto-build
✔ Security checks
✔ Linting
✔ Docker validation

---

## 🛡 Security Overview

✔ OTP verification for applicants
✔ Hashed employer passwords
✔ Flask-Login session authentication
✔ Rate limiting to defend login endpoints
✔ No direct database exposure
✔ Rejection emails sent from **no-reply** ID
✔ CSRF protection for forms

---

## 👥 Contributing

Contributions are welcome!
Read our guide → `CONTRIBUTING.md`

Steps:

1️⃣ Fork repo
2️⃣ Create feature branch
3️⃣ Submit a PR ✔️

---

## 📜 License

Licensed under the **MIT License**
See `LICENSE` file for more details.

---

## ❤️ Credits

Developed by **BIBIN N BIJI**
Give the project a ⭐ star if you find it useful!

---

## 🌐 Future Enhancements

🔹 PostgreSQL database support
🔹 Admin analytics dashboard
🔹 Resume PDF viewer
🔹 Multi-role authorization
🔹 JWT API mode for mobile app support

---


