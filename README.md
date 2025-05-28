# Secure Job Portal Application (Flask + OTP + Employer Dashboard)

This is a full-stack Flask-based secure job application system with the following key features:

---

✅ FEATURES

- OTP-secured email verification before application submission
- Employer-only dashboard protected by login
- JSON-based data storage for all job applications
- Rejection button sends a no-reply system-generated email
- Flask-Login for session and role security
- Rate limiting to prevent brute-force login attempts
- Docker support for easy containerized deployment

---

🗂️ PROJECT STRUCTURE

job_portal_app/
├── static/
│   └── style.css               # Common CSS
├── templates/
│   ├── dashboard.html          # Employer dashboard
│   ├── otp_verify.html         # OTP input page
│   ├── career.html             # Job application form
│   ├── login.html              # Employer login
├── data/
│   └── applications.json       # Stored job applications
├── app.py                      # Flask backend
├── Dockerfile                  # Docker container definition
├── requirements.txt            # Python package list
└── README.md                   # Project documentation

---

🚀 RUNNING LOCALLY

1. Clone the Repository:

   git clone https://github.com/yourname/job_portal_app.git
   cd job_portal_app

2. Install Dependencies:

   pip install -r requirements.txt

3. Start Flask Server:

   python app.py

Open your browser and visit: http://localhost:5000

---

🐳 RUNNING WITH DOCKER

1. Build Docker Image:

   docker build -t jobportal .

2. Run the Container:

   docker run -p 5000:5000 jobportal

---

🧪 EMPLOYER LOGIN

Email: employer@example.com  
Password: securepassword

---

📧 SMTP EMAIL SETUP

In app.py, locate and update this code block with your actual SMTP credentials:

   with smtplib.SMTP("smtp.yourmail.com", 587) as server:
       server.login("your-email@example.com", "your-password")

Example for Gmail:
- SMTP: smtp.gmail.com
- Port: 587
- Use an App Password if 2FA is enabled (https://support.google.com/accounts/answer/185833)

---

🛡️ SECURITY OVERVIEW

- Flask-Login for authenticated sessions
- Hashed passwords for employer login
- OTP-based email verification for applicants
- JSON-based secure application storage
- Rate limiting to defend against brute-force attacks
- No-reply rejection emails ensure professionalism and non-interaction

---

📜 LICENSE

MIT License – use freely with credit.

---

🤝 CONTRIBUTING

Pull requests welcome. Please open an issue for major changes or ideas.
