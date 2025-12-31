

# 🛡️ Cybersecurity Intern Task 1

## Web Application Security Assessment Report

---

**Tester Name:** Newaz Nezif
**Role:** Cybersecurity Intern
**Date:** December 18, 2025

---

## 📌 Overview

This repository documents a hands-on web application security assessment conducted against **OWASP Juice Shop**, an intentionally vulnerable application designed for learning and practicing web security testing.

The assessment follows **OWASP Top 10 (2021)** guidelines and combines **manual testing** with **automated scanning** using **OWASP ZAP**.
All testing was performed in a **controlled local environment** for **educational purposes only**.

---

## ⚙️ Environment Setup

### Operating Environment

* **Operating System:** Linux (Ubuntu-based)
* **Architecture:** x64
* **User Privileges:** Standard user with sudo access
* **Testing Scope:** Local, non-production environment

---

## 🐳 Docker Installation & Configuration

Docker was used to ensure a consistent and isolated runtime environment.

### Steps Performed

* Installed Docker Engine
* Verified Docker service status
* Pulled and ran the official OWASP Juice Shop image

```bash
docker run -d -p 3000:3000 bkimminich/juice-shop
```

### Outcome

* Application deployed successfully in a Docker container
* Accessible locally at:
  **[http://localhost:3000](http://localhost:3000)**

---

## 🧬 Source Code Setup (GitHub)

To analyze the application structure and behavior, the source code was cloned locally.

* **Repository:** [https://github.com/juice-shop/juice-shop](https://github.com/juice-shop/juice-shop)

```bash
git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
```

### Outcome

* Full source code downloaded
* Local development environment prepared for testing

---

## 🟢 Node.js & Dependency Setup

OWASP Juice Shop requires Node.js to run from source.

### Actions Taken

* Updated Node.js to **v20**
* Installed dependencies using npm

```bash
node -v
npm -v
npm install
```

### Outcome

* Dependencies installed successfully
* No critical build errors encountered

---

## ▶️ Application Build & Execution

```bash
npm start
```

### Outcome

* Application started successfully
* Server running on **port 3000**
* Console logs confirmed proper initialization

---

## 🔍 Security Testing Tool Setup

### OWASP ZAP Configuration

* Installed and launched OWASP ZAP
* Browser traffic routed through ZAP proxy
* Target added: **[http://localhost:3000](http://localhost:3000)**

---

## ✅ Environment Validation

Before testing, the following checks were completed:

* Application reachable in browser
* Docker container running
* ZAP proxy intercepting traffic
* Manual interaction successful

✔️ Environment confirmed ready for assessment.

---

## 🧠 Why This Setup Matters

This setup ensures:

* Ethical and legal testing
* Reproducible results
* Isolation from real-world systems
* Alignment with OWASP testing best practices

---

## 📊 Executive Summary

This assessment identified multiple security vulnerabilities, including **Cross-Site Scripting (XSS)** and **Security Misconfigurations**. These weaknesses could allow attackers to execute malicious scripts, manipulate application behavior, or compromise user data.

All findings are documented with:

* Risk ratings
* OWASP Top 10 mappings
* Impact analysis
* Remediation recommendations

This report simulates a real-world client security engagement.

---

## 🎯 Scope of Assessment

### In Scope

* Web application at `http://localhost:3000`
* Client-side vulnerabilities (e.g., XSS)
* Server-side vulnerabilities
* Input fields and URL parameters
* Authentication-independent endpoints

### Out of Scope

* Denial of Service (DoS)
* Infrastructure-level attacks
* Brute-force attacks
* Social engineering
* Network-level exploitation

---

## 🛠️ Tools & Methodology

### Tools Used

| Tool             | Purpose                          |
| ---------------- | -------------------------------- |
| OWASP Juice Shop | Vulnerable test application      |
| OWASP ZAP        | Automated vulnerability scanning |
| Web Browser      | Manual testing                   |

### Testing Phases

1. Application setup
2. Reconnaissance
3. Manual testing
4. Automated scanning
5. Analysis and validation
6. OWASP Top 10 mapping

---

## 🧪 Manual Testing Findings

### 🔴 Vulnerability 1: Cross-Site Scripting (XSS)

* **Risk Level:** High

**Description:**
A reflected XSS vulnerability was identified in the search functionality due to unsanitized user input.

**Payload Examples:**

```html
<img src="invalid" onerror="alert('Successful XSS')">
<details open ontoggle="alert('XSS')"></details>
```

**Impact:**

* Session hijacking
* Credential theft
* Malicious redirects
* Arbitrary JavaScript execution

**OWASP Mapping:**

* A03:2021 – Injection ❌

---

### 🟠 Vulnerability 2: Improper Error Handling / Access Control

* **Risk Level:** Medium

Unauthenticated access to the basket endpoint:

```
http://localhost:3000/#/basket
```

**Impact:**

* Information disclosure
* Increased attack surface
* Reveals internal application behavior

**OWASP Mapping:**

* A05:2021 – Security Misconfiguration ❌

---

## 🤖 Automated Scan Results (OWASP ZAP)

### Key Findings

* Missing Content Security Policy (CSP)
* Missing Anti-clickjacking headers
* Vulnerable JavaScript libraries
* Missing HSTS header
* Session ID exposed in URL
* Information disclosure
* Server version leakage

---

## 🚨 Notable Vulnerabilities

### Vulnerability 3: Missing CSP

* **Risk:** Medium
* **Confidence:** High

### Vulnerability 4: CORS Misconfiguration

* **Risk:** Medium
* **Confidence:** Medium

### Vulnerability 5: Missing Anti-clickjacking Header

* **Risk:** Medium
* **Confidence:** Medium

### Vulnerability 6: Session ID in URL Rewrite

* **Risk:** Medium
* **Confidence:** High

---

## 🌐 Endpoint Exposure

| Endpoint        | Risk   | Description                    |
| --------------- | ------ | ------------------------------ |
| `/ftp`          | High   | Information disclosure         |
| `/api`, `/rest` | Medium | CORS misconfiguration          |
| `/socket.io/`   | High   | Session ID in URL              |
| `robots.txt`    | Medium | Reconnaissance data            |
| `sitemap.xml`   | Medium | Application structure exposure |

---

## 🗂️ OWASP Top 10 Mapping Summary

| Vulnerability  | OWASP Category                       |
| -------------- | ------------------------------------ |
| XSS            | A03:2021 – Injection                 |
| Error Handling | A05:2021 – Security Misconfiguration |
| Missing CSP    | A05:2021                             |
| CORS Misconfig | A05:2021                             |
| Clickjacking   | A05:2021                             |
| Session in URL | A07:2021                             |
| Outdated JS    | A06:2021                             |

---

## 🏁 Conclusion

This assessment successfully identified multiple real-world vulnerabilities commonly found in modern web applications. The most critical issues stem from **Security Misconfigurations** and **Client-Side Injection flaws**, emphasizing the need for defense-in-depth strategies.

Key takeaways:

* Importance of secure headers (CSP, HSTS, X-Frame-Options)
* Risks of exposing session IDs in URLs
* Value of combining manual and automated testing
* Practical experience with OWASP methodologies

If deployed in production, these vulnerabilities could result in data compromise, session hijacking, and user exploitation. Immediate remediation is strongly recommended.

---

## 🙌 Acknowledgment

Thank you for reviewing this assessment.
This project represents hands-on learning in ethical hacking, vulnerability assessment, and professional security reporting.

---

