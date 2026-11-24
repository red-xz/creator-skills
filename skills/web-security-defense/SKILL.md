---
name: web-security-defense
description: Defensive web security for a creator's own website — OWASP Top 10:2025, hardening checklists, and responsible disclosure. Use when auditing or hardening a site you own. No offensive content: this skill is defense only.
---

# Web Security — Defense Only

This skill is for protecting a website you own. It covers what the risks
are, how to harden a site, and how to handle a vulnerability report. It
does not teach attacking other people's systems, and nothing in it should
be used on a system you do not own or have written permission to test.

## Hard boundary

- **Authorized testing only:** test systems you own, or systems with
  written, scoped permission from someone with authority over them
  (specific systems, techniques, time window).
- Authorization is the only difference between a security audit and a
  crime. Same technique, lawful with permission, criminal without. Good
  intentions and reporting afterwards do NOT retroactively make
  unauthorized access lawful.
- A vulnerability disclosure policy is NOT authorization to test.
- Laws (plain language): US CFAA, UK Computer Misuse Act, Canada Criminal
  Code s.342.1 — unauthorized access is a crime in most jurisdictions.
- Practice only on: systems you own, systems with written authorization,
  or platforms with an explicit invitation to test (OWASP Juice Shop,
  DVWA, PortSwigger labs, TryHackMe, HackTheBox).

## OWASP Top 10:2025 (current edition, verified at top10.owasp.org/2025)

1. A01 Broken Access Control (still #1; now includes SSRF)
2. A02 Security Misconfiguration (up from #5)
3. A03 Software Supply Chain Failures (new; expanded from old A06)
4. A04 Cryptographic Failures
5. A05 Injection (SQLi, XSS, OS command, LDAP, NoSQL)
6. A06 Insecure Design
7. A07 Authentication Failures
8. A08 Software or Data Integrity Failures
9. A09 Security Logging and Alerting Failures
10. A10 Mishandling of Exceptional Conditions (new — errors/abnormal
    states leak data or fail open)

Related standards: OWASP WSTG v4.2 (testing guide), OWASP ASVS 5.0 (345
requirements).

## How an audit runs (when checking your own site)

- **Pre-engagement:** scope + written authorization + rules of engagement
  agreed first. Then intelligence gathering, threat modeling,
  vulnerability analysis, authorized verification, and reporting — plus a
  remediation retest after fixes.
- **Report contents:** executive summary (plain language, business risk),
  scope & rules of engagement, methodology, findings table, detailed
  findings (severity + CVSS, affected asset, evidence/reproduction,
  impact, remediation), remediation plan by priority, retest results.
  Typical timelines: Critical 24–48h, High 1 week, Medium 30 days, Low
  90 days.
- Active scanners can slow or break a live site — run them against a
  STAGING copy, with a backup, only on authorized sites.

## Defensive tools (free, what each does)

- **Nmap** — network discovery, port/service scanning, OS detection. Use
  on your own network to see what is exposed.
- **OWASP ZAP** — free open-source web app scanner + proxy; baseline scan
  is passive/safe. The first scanner to run on your own site.
- **Burp Suite Community Edition** — free intercepting proxy (Proxy,
  Repeater, Decoder); no automated scanner (Pro $499/yr).
- **Nikto** — web server scanner, 6,700+ checks; noisy/active — staging
  only.
- **WPScan** — WordPress scanner (core/plugins/themes/users vs
  vulnerability DB). Free CLI; free non-commercial API token (25
  req/day); maintained by Automattic.
- **testssl.sh** — TLS configuration checks.
- **Wappalyzer / WhatWeb** — technology fingerprinting (see what your own
  site reveals about its stack).
- **Nuclei** (template scanner), **Greenbone/OpenVAS** (vulnerability
  management), **Wireshark** (inspect HTTP/TLS, spot cleartext
  credentials on your own network).
- **Kali Linux** bundles most of these — but a scanner in the wrong hands
  is an attack tool. Everything above is for your own systems and labs.

## Learning resources & labs (legal practice)

- **PortSwigger Web Security Academy** (portswigger.net/web-security) —
  FREE, ~31 topics, ~273 labs. The core learning path. BSCP exam $99.
- **TryHackMe** — guided rooms/paths; free tier; Premium ~$10–14/mo
  (prices vary by source — check vendor).
- **HackTheBox** — unguided machines; free tier; VIP+ $25/mo. HTB Academy
  separate.
- Intentionally vulnerable apps (run locally/host-only, NEVER on a public
  network): OWASP Juice Shop (100+ challenges), DVWA (adjustable
  difficulty), OWASP WebGoat, Metasploitable, VulnHub.
- Free courses: Google Cybersecurity Certificate (Coursera, ~$49/mo),
  freeCodeCamp Ethical Hacking (YouTube, free), Cisco Intro to
  Cybersecurity (free, 15h).
- Certifications (2026 prices, verify before buying): eJPT ~$249 (best
  first defensive/offensive cert), CompTIA Security+ $439, PenTest+ $439,
  CEH $950–$1,199, OSCP $1,749 (24-hr hands-on exam), PNPT $499.

## Hardening checklist — WordPress

From the official WordPress hardening guide:

- Updates: core/plugins/themes current; auto-updates on; delete unused
  plugins/themes.
- Passwords: long, unique; no "admin" username; least-privilege roles;
  2FA for all admins/editors.
- wp-config.php: DISALLOW_FILE_EDIT, unique salts/keys, restricted DB
  user, file perms 400/440, only wp-content writable by web server.
- HTTPS everywhere (Let's Encrypt); FORCE_SSL_ADMIN.
- Login protection: limit attempts, disable XML-RPC/pingbacks if unused,
  generic login errors, block user enumeration (/?author=N).
- WAF: host/CDN (Cloudflare, Sucuri) or plugin (Wordfence); security
  plugins: Wordfence, Sucuri, MalCare.
- Backups: automatic, off-site, TESTED restores.
- Monitoring: activity log, file-change detection, wp core
  verify-checksums (WP-CLI), Search Console.

## Hardening checklist — general (OWASP HTTP Headers Cheat Sheet)

- HSTS: `Strict-Transport-Security: max-age=63072000; includeSubDomains;
  preload` (roll out with short max-age first).
- CSP: strict nonce/hash-based policy; start in Report-Only;
  `frame-ancestors 'none'` replaces X-Frame-Options.
- `X-Frame-Options: DENY` (fallback), `X-Content-Type-Options: nosniff`,
  `Referrer-Policy: strict-origin-when-cross-origin`,
  `Permissions-Policy: geolocation=(), camera=(), microphone=()`.
- Remove X-Powered-By and versioned Server headers; do NOT set
  X-XSS-Protection (deprecated); drop Expect-CT.
- Cookies: Secure; HttpOnly; SameSite=Lax. TLS 1.2+ only.
- General: strong passwords + 2FA, least privilege, patching, tested
  backups, WAF, logging/monitoring, server-side input validation, CSRF
  tokens, secure uploads (type/size checks, store outside web root, never
  execute).

## Responsible disclosure (when someone reports a bug to you)

- Report privately to the owner first (security@ or security.txt);
  include system/URL, description, date/time, impact, contact info; NO
  passwords/PII; no extra testing to prepare the report; give time to fix
  before any public disclosure; never threaten or demand payment outside
  a bounty program.
- If you receive a report: acknowledge it, fix on the severity timeline
  above, and retest. A reporter who went private first is doing you a
  favour.

## Defensive lessons from public incidents

Distilled from public post-mortems of major breaches (including Binance's
2019, 2022, and October 2026 incidents, per their public reports). No
attack detail — only what a site owner should do differently:

- Phishing-resistant MFA (hardware keys beat SMS codes); least-privilege
  API keys; withdrawal/rate/velocity caps on money-moving actions.
- Verify EVERY field of user-supplied data and proofs — partial
  verification is how bypasses happen.
- Aggregate anomaly detection, not just per-transaction checks — a
  coordinated action can pass every single check.
- A tested kill switch: the ability to halt a service fast, practised
  before you need it.
- Secrets out of repos; never run untrusted code on credential-holding
  machines; verify software installers (supply-chain compromise is a
  real entry point).
- Separate privileged operations: signing/approval services isolated,
  multi-party approval for sensitive actions.
- Vendor review; bug bounty; an incident plan; an emergency fund
  (SAFU-style reserve); freeze-first, disclose-fast; public post-mortems.

## Before auditing a site

1. Ask: platform (WordPress/custom/Shopify), hosting, admin access (via
   a secure channel, never in chat), and written confirmation that it is
   your site and you may test it.
2. Fingerprint (WhatWeb/Wappalyzer), then run passive checks first
   (headers, TLS, version exposure).
3. Run the matching hardening checklist; run WPScan (WordPress) or a ZAP
   baseline scan (custom) against a staging copy if one exists.
4. Report findings in plain language, ranked by severity, with fixes —
   and fix what is approved.
