# 🔐 DevSecOps — OWASP ZAP Portfolio Security Scan

![DevSecOps](https://img.shields.io/badge/DevSecOps-ZAP%20Scan-blue)
![OWASP ZAP](https://img.shields.io/badge/Tool-OWASP%20ZAP%20by%20Checkmarx-red)
![DAST](https://img.shields.io/badge/Testing-DAST-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey)

---

## 📌 What is this project?

This repository documents a real-world **DAST (Dynamic Application Security Testing)** scan performed on my personal portfolio website using **OWASP ZAP (Zed Attack Proxy) by Checkmarx**.

As part of my DevSecOps learning journey, I wanted to go beyond theory and test an actual live web application for security vulnerabilities — the same way security engineers do in real organizations.

> **Target:** Personal Portfolio — [https://ayansaiyad.vercel.app](https://ayansaiyad.vercel.app)  
> **Tool:** OWASP ZAP 2.17.0 by Checkmarx  
> **Scan Type:** DAST (Dynamic Application Security Testing)  
> **Date:** June 2026

---

## ❓ Why DAST?

DAST tests a **running application from the outside** — just like a real attacker would. It does not require access to source code.

| Testing Type | What it does | When |
|---|---|---|
| SAST | Scans source code | Before build |
| DAST | Scans running application | After deployment |
| **ZAP** | **DAST tool — scans live web apps** | **In production/staging** |

In DevSecOps, DAST is a critical part of the **Shift Left** approach — finding vulnerabilities before they become real threats.

---

## 🛠️ What is OWASP ZAP?

**OWASP ZAP (Zed Attack Proxy)** is a free, open-source security testing tool maintained by **Checkmarx**. It is one of the most widely used tools for finding vulnerabilities in web applications.

It works by acting as a **proxy between your browser and the web application**, intercepting and analyzing all requests and responses to find security flaws.

🔗 Official Website: [https://www.zaproxy.org](https://www.zaproxy.org)

---

## ⚙️ How to Install OWASP ZAP

### 🪟 Windows (Detailed)

1. Go to [https://www.zaproxy.org/download](https://www.zaproxy.org/download)
2. Click **"Windows Installer"** and download the `.exe` file
3. Run the installer as **Administrator**
4. Follow the setup wizard — click Next → Next → Install
5. Once installed, launch **ZAP** from the Start Menu
6. On first launch, select **"No, I do not want to persist this session"** → Start
7. ZAP is ready to use ✅

### 🐧 Ubuntu (Short)

```bash
sudo apt update
sudo apt install zaproxy -y
zaproxy
```

### 🍎 Mac (Short)

```bash
brew install --cask owasp-zap
```

---

## 🚀 How I Ran the Scan

1. Opened OWASP ZAP on Windows
2. Selected **"Automated Scan"** from Quick Start tab
3. Entered target URL: `https://ayansaiyad.vercel.app`
4. Clicked **"Attack"**
5. ZAP ran Spider + Active Scan automatically
6. Reviewed all findings in the **Alerts** tab

---

## 📊 Scan Results Summary

| Risk Level | Count |
|---|---|
| 🔴 High | 0 |
| 🟡 Medium | 3 |
| 🔵 Low | 2 |
| ℹ️ Informational | 3 |
| **Total Alerts** | **8** |

---

## 🔍 Findings

### 🟡 Medium Risk

**1. Content Security Policy (CSP) Header Not Set**
- CSP headers tell the browser which sources of content are trusted
- Without it, the site is vulnerable to **XSS (Cross-Site Scripting)** and **data injection attacks**
- CWE: 693 | WASC: 15

**2. Missing Anti-Clickjacking Header**
- X-Frame-Options header is not set
- Without it, attackers can embed the site inside an invisible iframe to trick users — known as **Clickjacking**
- CWE: 1021

**3. Cross-Domain Misconfiguration**
- `Access-Control-Allow-Origin: *` is set
- This allows **any domain** to make requests to the site — potential data exposure risk

### 🔵 Low Risk

**4. X-Content-Type-Options Header Missing**
- Without this header, browsers may **MIME-sniff** responses and execute files as a different type than intended

**5. Timestamp Disclosure - Unix**
- Server is exposing internal timestamps in HTTP responses
- Can reveal server information to attackers

### ℹ️ Informational

- Modern Web Application detected
- Re-examine Cache-control Directives
- Retrieved from Cache

---

## 📸 Screenshots

| Description | File |
|---|---|
| ZAP Alerts Overview | `screenshots/zap-alerts-report.png` |
| ZAP Scan Running | `screenshots/zap-scan-running.png` |

---

## 📂 Repository Structure

```
devsecops-zap-portfolio-scan/
│
├── README.md
├── screenshots/
│   ├── zap-alerts-report.png
│   └── zap-scan-running.png
│
└── reports/
    └── zap-scan-report.html
```

---

## 🔄 Next Steps

- [ ] Fix CSP Header via `vercel.json`
- [ ] Add X-Frame-Options Header
- [ ] Add X-Content-Type-Options Header
- [ ] Re-scan after fixes to verify remediation
- [ ] Integrate ZAP into GitHub Actions CI/CD pipeline

---

## 💡 Key Takeaway

> *"Security isn't the last step — it's every step."*

Even a simple static portfolio has security gaps. A DevSecOps engineer's job is to **Find it. Document it. Report it. Fix it.**

---

## 👨‍💻 Author

**Ayan Saiyad** — Aspiring DevSecOps Engineer  
6 months DevOps Internship completed. Now focused on DevSecOps — securing pipelines, one scan at a time. 🚀

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/)
[![Portfolio](https://img.shields.io/badge/Portfolio-Live-green)](https://ayansaiyad.vercel.app/)
