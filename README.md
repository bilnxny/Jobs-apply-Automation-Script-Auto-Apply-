# 🤖 CyberJobs Auto-Applier

> Automated LinkedIn job application bot built for **cybersecurity professionals** — VAPT, Penetration Testing, SOC Analyst, Red Team, and Bug Bounty roles.

[![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Playwright](https://img.shields.io/badge/Playwright-45ba4b?style=for-the-badge&logo=playwright&logoColor=white)](https://playwright.dev)
[![License](https://img.shields.io/badge/License-MIT-c00020?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-00c853?style=for-the-badge)](#)

---

## 📖 Overview

**CyberJobs Auto-Applier** is a Python-based automation tool that applies to cybersecurity jobs on LinkedIn automatically. Built specifically for security professionals tired of manually applying to hundreds of listings.

**Built for:**
- 🎯 VAPT Analysts
- 🔐 Penetration Testers
- 🛡️ SOC Analysts
- ⚔️ Red Team Operators
- 🐛 Bug Bounty Hunters
- 🔍 Application Security Engineers

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| **🎯 Smart Job Filtering** | Filters by role title, location, remote-only, and Easy Apply availability |
| **🤖 Auto-Apply Engine** | Handles multi-step forms, uploads resume, submits applications |
| **🌍 Worldwide Search** | Configurable location targeting (India, US, EU, Remote, Worldwide) |
| **🔒 Anti-Detection** | Randomized delays, human-like scrolling, session persistence |
| **📊 Application Tracking** | Logs every application with timestamp, company, and status |
| **♻️ Daily Runs** | Run once a day → 30–50 applications auto-submitted |
| **⚡ Playwright-Based** | Faster and more reliable than Selenium |
| **🛠️ Fully Configurable** | Change search terms, apply limits, and filters via simple config |

---

## ⚙️ Tech Stack

- **Python 3.9+** — Core logic
- **Playwright** — Browser automation
- **CSV / JSON** — Application logging
- **Gmail SMTP** — Optional cold-email outreach

---

## 🚀 Quick Start

### 1. Clone the Repo

```bash
git clone https://github.com/bilnxny/cyberjobs-auto-applier.git
cd cyberjobs-auto-applier
```

### 2. Install Dependencies

```bash
pip install playwright
playwright install chromium
```

### 3. Configure

Edit `config.py`:

```python
EMAIL = "your.email@gmail.com"
PASSWORD = "your_password"
MAX_APPLICATIONS = 30
SEARCHES = [
    "VAPT Analyst",
    "Penetration Tester",
    "Cyber Security Analyst",
    "SOC Analyst",
    "Red Team Operator",
]
LOCATION = "Worldwide"
REMOTE_ONLY = True
```

### 4. Run

```bash
python auto_apply.py
```

Browser opens → logs in → applies to 30 jobs in ~15 minutes.

---

## 📂 Project Structure

```
cyberjobs-auto-applier/
├── auto_apply.py          # Main application bot
├── bulk_email.py          # Cold email sender (optional)
├── config.py              # Configuration file
├── requirements.txt       # Dependencies
├── applications.csv       # Auto-generated log
├── resume.pdf             # Your resume (gitignored)
├── .gitignore
└── README.md
```

---

## 🎯 How It Works

```
1. Opens Chromium via Playwright
2. Logs into LinkedIn with stored credentials
3. For each search term:
   - Searches jobs on LinkedIn
   - Filters: Easy Apply + Remote + Location
   - For each job:
     - Opens listing
     - Clicks "Easy Apply"
     - Fills multi-step form
     - Uploads resume (if requested)
     - Submits application
     - Logs to applications.csv
4. Closes browser after MAX_APPLICATIONS reached
```

---

## 📊 Application Log Format

Every application is logged to `applications.csv`:

```csv
date,time,job_title,company,location,status,url
2026-09-21,09:14:33,Penetration Tester,CrowdStrike,Remote,Applied,https://linkedin.com/jobs/...
2026-09-21,09:16:12,VAPT Analyst,Palo Alto Networks,Remote,Applied,https://linkedin.com/jobs/...
```

---

## 🔧 Configuration Options

| Option | Default | Description |
|--------|---------|-------------|
| `MAX_APPLICATIONS` | 30 | Max jobs to apply per run |
| `SEARCHES` | 5 terms | Job titles to search |
| `LOCATION` | Worldwide | Target location |
| `REMOTE_ONLY` | True | Only remote jobs |
| `HEADLESS` | False | Run browser in background |
| `DELAY_MIN` | 3 | Min seconds between apps |
| `DELAY_MAX` | 6 | Max seconds between apps |

---

## ⚠️ Important Safety Notes

### LinkedIn Rate Limits
- **Max 30 apps/day** — more will trigger bot detection
- **Never run more than once per 24 hours** on the same account
- **Test on a dummy account first** before using your main profile

### Account Safety
- Use **headless=False** on first run to watch behavior
- **Never commit your password** to Git — use environment variables
- Consider using **2FA + App Password** setup
- If LinkedIn warns you → **stop immediately** for 48 hours

### Legal & Ethical
- This tool is for **personal use only**
- **Do NOT** use for mass spam or reselling
- **Do NOT** scrape other users' data
- Check LinkedIn's **Terms of Service** before using — automation violates ToS and could result in account restriction

---

## 🛡️ Anti-Detection Techniques

The bot includes these built-in safeguards:

- ✅ Random delays between actions (3–6 seconds)
- ✅ Human-like scroll patterns
- ✅ Realistic user-agent string
- ✅ Persistent browser session (keeps cookies)
- ✅ Skip-if-already-applied detection
- ✅ Daily application cap
- ✅ Natural mouse movement simulation

---

## 📈 Results (Typical Run)

| Metric | Value |
|--------|-------|
| **Jobs scanned** | 200–400 |
| **Jobs applied** | 25–35 |
| **Time taken** | 12–18 min |
| **Success rate** | 90%+ |

---

## 🧪 Testing Checklist

Before daily use:

- [ ] Run with `headless=False` first (watch the bot)
- [ ] Verify login works
- [ ] Test with `MAX_APPLICATIONS = 3`
- [ ] Check `applications.csv` gets populated
- [ ] Verify resume uploads correctly
- [ ] Confirm no duplicate applications

---

## 🛠️ Troubleshooting

| Issue | Fix |
|-------|-----|
| **Login fails** | LinkedIn may require CAPTCHA — solve manually once, then bot uses saved session |
| **Easy Apply button not found** | Some jobs use external apply; bot skips them |
| **Form submission fails** | Job may have custom questions — add answers in `config.py` |
| **Rate limited** | Reduce `MAX_APPLICATIONS`, wait 24 hours |
| **Browser crashes** | Update Playwright: `playwright install --force` |
| **Resume not uploading** | Ensure `resume.pdf` exists in project root |

---

## 📦 requirements.txt

```
playwright==1.40.0
pandas==2.1.0
python-dotenv==1.0.0
```

---

## 🔒 .gitignore

```
resume.pdf
applications.csv
*.log
.env
config_local.py
__pycache__/
*.pyc
.playwright/
```

---

## 🚧 Roadmap

- [ ] Multi-platform support (Naukri, Indeed, Hirist.tech)
- [ ] AI-based cover letter generation
- [ ] Gmail auto-follow-up for HR responses
- [ ] Web dashboard for application tracking
- [ ] Resume matching score before applying
- [ ] Telegram notifications on successful applications

---

## 🤝 Contributing

Pull requests welcome. For major changes:

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/NewFeature`)
3. Commit changes (`git commit -m 'Add NewFeature'`)
4. Push (`git push origin feature/NewFeature`)
5. Open a Pull Request

---

## 📜 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Muhammed Bilal TA**
- 🌐 Portfolio: [bilnxny.github.io](https://bilnxny.github.io)
- 💻 GitHub: [@bilnxny](https://github.com/bilnxny)
- 📧 Email: muhanmedbilallalu@gmail.com
- 🎯 Role: Cyber Security Analyst · VAPT Specialist

---

## ⚠️ Disclaimer

This project is for **educational purposes** and **personal job-search automation**. 

- The author is **not responsible** for any account restrictions or bans
- Automation may violate LinkedIn's **Terms of Service** — use at your own risk
- **Never** share your credentials publicly
- **Never** use for spam or commercial scraping
- **Always** respect platform rate limits

> By using this tool, you acknowledge that you understand and accept these risks.

---

<div align="center">

**⭐ If this tool helped you land a job, star the repo!**

Made with ☕ + 🐍 + 🛡️ from Kerala, India

</div>
