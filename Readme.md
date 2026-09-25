# Secure SDLC & DevSecOps Assessment Specification (CryptoV4ult)

A conceptual DevSecOps security assessment framework, threat modeling study, and secure Software Development Lifecycle (SDLC) implementation blueprint for a simulated cryptocurrency platform (CryptoV4ult).

---

## Scope & Purpose

* **Target Platform:** CryptoV4ult (a simulated cryptocurrency exchange and wallet platform).
* **Objective:** Map automated security verification gates across Design, Build, Test, and Deploy phases.
* **Classification:** Architectural specification and DevSecOps governance checklist. This repository contains engineering documentation rather than an executable application codebase.

---

## Secure SDLC Stages & Automated Security Gates

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ 1. DESIGN    │ ──> │ 2. BUILD     │ ──> │ 3. TEST      │ ──> │ 4. DEPLOY    │
│ Threat Model │     │ SAST Linting │     │ DAST Scans   │     │ Runtime Hard │
│ OWASP ASVS   │     │ SonarQube    │     │ OWASP ZAP    │     │ Trivy Scans  │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
```

### 1. Requirements & Threat Modeling (Design Phase)
* **Threat Modeling:** Identification of attack surfaces across public REST endpoints, internal wallet services, and database layers using STRIDE.
* **Architecture Security Standard:** Enforcing OWASP Application Security Verification Standard (ASVS) Level 2 requirements for authentication and session management.

### 2. Static Code Analysis & Secret Scanning (Build Phase)
* **SAST Integration:** Automated source code analysis targeting SQL injection, unsafe deserialization, and hardcoded secrets (modeling tools such as SonarQube and Bandit).
* **Pre-Commit Hooks:** Local git hook validation preventing API keys, private certificates, or seed phrases from entering repository history.

### 3. Dynamic Application Security Testing & API Audits (Test Phase)
* **DAST Assessments:** Automated vulnerability scanning of running staging environments using OWASP ZAP.
* **API Security Top 10 Auditing:** Specialized testing for Broken Object Level Authorization (BOLA/IDOR), rate limit bypasses on login endpoints, and excessive data exposure in JSON payloads.

### 4. Container & Infrastructure Security (Package & Deploy Phase)
* **Container Image Scanning:** Static analysis of Docker base images for known Common Vulnerabilities and Exposures (CVEs) modeling Trivy.
* **Least-Privilege Container Configuration:** Enforcing non-root container users, read-only root filesystems, and minimal Alpine/distroless base images.

---

## Targeted Vulnerability Assessment & Remediation Matrix

| Assessment Domain | Simulated Vulnerability | Severity | Remediation Strategy |
| :--- | :--- | :--- | :--- |
| **Authentication** | Missing rate-limiting on `/api/v1/auth/login` | High | Implement Redis-backed token bucket rate limiting (max 5 failed attempts per 15 min). |
| **Session Security** | JWT tokens stored in browser `localStorage` | Medium | Migrate session tokens to secure, `HttpOnly`, `SameSite=Strict` cookies. |
| **API Endpoints** | IDOR vulnerability on user transaction records | High | Enforce server-side tenancy validation: verify requesting JWT `sub` owns transaction `id`. |
| **Container Image** | Vulnerable OpenSSL package in Docker base image | Critical | Pin verified base image digest and automate base image rebuilding on CVE alerts. |

---

## Project Status & Classification

* **Project Type:** Conceptual Security Framework & SDLC Governance Specification.
* **Implementation Note:** This repository documents an architectural blueprint and assessment methodology. It serves as an engineering case study for integrating security controls into development pipelines, rather than an executable application codebase.

---

## Author & Links

* **Author:** Siddh Samarth
* **GitHub:** [@SiddhSamarth](https://github.com/SiddhSamarth)
* **Portfolio:** [siddhsamarth.in](https://siddhsamarth.in)
* **LinkedIn:** [samarthsiddh](https://www.linkedin.com/in/siddhsamarth/)
