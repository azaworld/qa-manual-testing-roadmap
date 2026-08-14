# Stage 13 — Security Testing for QA

> **Goal:** find the security bugs that ordinary functional testing walks right past. You don't need to be a pentester — you need the OWASP mindset and a handful of manual techniques that catch the most common, most damaging holes. I ran security-critical QA at Mastercard; these are the checks that matter.

> ⚠️ **Ethics & scope first.** Only test systems you own or are explicitly authorized to test. Unauthorized testing is illegal. Everything here is for your own apps, staging environments, and the deliberately-vulnerable practice targets listed at the end.

## 1. The security mindset

Functional testing asks *"does it work?"* Security testing asks *"what can a malicious user make it do?"* Every input is a potential weapon; every response is a potential leak; every permission is a potential bypass.

## 2. The OWASP Top 10 — a QA's field guide

The [OWASP Top 10](https://owasp.org/www-project-top-ten/) is THE reference. What each means and how you test it manually:

| Risk | What it is | Manual test |
|---|---|---|
| **Broken Access Control** | Users reaching data/actions they shouldn't | Log in as user A, grab a resource URL/ID, request it as user B (**IDOR**). Change `role=user` to `role=admin` in requests. #1 most common real bug |
| **Cryptographic Failures** | Sensitive data exposed | Is traffic HTTPS everywhere? Passwords/tokens in URLs, logs, or responses? PII in JWTs? |
| **Injection** | Untrusted input hits an interpreter | `' OR '1'='1` in inputs (SQLi); `<script>alert(1)</script>` (XSS); command strings. Watch for raw echo-back or DB errors |
| **Insecure Design** | Missing security controls by design | No rate limit on login/OTP? No lockout? Password reset that reveals if an email exists? |
| **Security Misconfiguration** | Defaults, verbose errors, open dirs | Stack traces shown to users, default creds, directory listing, missing security headers |
| **Vulnerable Components** | Outdated libraries | Check known-CVE versions (often visible in headers or JS bundles) |
| **Auth Failures** | Weak session/credential handling | Session survives logout? Predictable tokens? Weak-password policy? MFA bypass? |
| **Data Integrity Failures** | Unverified updates/deserialization | Tampered payloads accepted? Unsigned auto-updates? |
| **Logging/Monitoring Failures** | Attacks leave no trace | Do failed logins/permission-denials get logged? (Ask the team) |
| **SSRF** | Server tricked into fetching attacker URLs | Fields that take URLs — can you point them at internal addresses? |

## 3. The manual techniques you'll actually use

### Access control (find these first — they're everywhere)
- **IDOR:** `/api/orders/1001` works for you — try `1002`, `1000`. Get someone else's data? Critical bug.
- **Privilege escalation:** intercept a request, change a role/permission/price field, replay it
- **Forced browsing:** navigate directly to `/admin` while logged in as a regular user

### Input attacks
- **XSS:** put `<script>alert(document.cookie)</script>` in every text field, name, comment, search box, and URL param. Reflected (echoed in response) or stored (saved and shown to others)?
- **SQLi:** `'`, `' OR '1'='1' --`, `1; DROP TABLE` — watch for DB errors, changed results, or timing differences
- **Template/command injection:** `{{7*7}}`, `${7*7}` — does `49` appear?

### The interceptor: Burp Suite / OWASP ZAP
The core skill. Point your browser through the proxy and you see + modify every request:
- **Intercept & modify:** change values the UI won't let you change (client-side validation is not security)
- **Repeater:** replay one request with tweaks — the workhorse for access-control testing
- **Spider/scan:** map the app and run automated checks (ZAP's free scanner is excellent for a first pass)

Free path: [OWASP ZAP](https://www.zaproxy.org/) is fully open-source; [Burp Suite Community](https://portswigger.net/burp/communitydownload) is free for manual work.

## 4. Security checks to add to every release

A lightweight checklist QA can own without being a security specialist:

- [ ] All traffic HTTPS; security headers present (CSP, HSTS, X-Frame-Options)
- [ ] Auth: lockout + rate limiting on login, OTP, password reset
- [ ] Access control: one IDOR probe per sensitive resource type
- [ ] Inputs: XSS probe on the top 5 user-facing fields
- [ ] Errors: no stack traces or internal details shown to users
- [ ] Sensitive data: not in URLs, logs, or API responses
- [ ] Session: invalidated on logout; cookies `HttpOnly` + `Secure`

## 5. Learn it properly (free, hands-on)

| Resource | What it gives |
|---|---|
| [PortSwigger Web Security Academy](https://portswigger.net/web-security) | THE free training — labs for every vuln class, made by the Burp team. Start here |
| [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) | Deliberately vulnerable app with a challenge scoreboard — practice legally |
| [OWASP crAPI](https://github.com/OWASP/crAPI) | API-focused vulnerable app (pairs with [Stage 12](13-api-testing-deep-dive.md)) |
| [OWASP Top 10 (read it)](https://owasp.org/www-project-top-ten/) | The canonical list, with examples |
| [OWASP WSTG](https://owasp.org/www-project-web-security-testing-guide/) | The Web Security Testing Guide — the professional checklist |
| [TryHackMe](https://tryhackme.com/) / [HackTheBox](https://www.hackthebox.com/) | Gamified hands-on security (some free) |
| [OWASP Top 10 for LLMs](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | AI-era security — prompt injection & friends (see [Stage 11](12-ai-for-qa.md)) |

## 6. When to escalate

You're the **first line**, not the last. When you find something serious: reproduce it, document it privately (never in a public tracker for a live vuln), classify impact, and escalate to security/engineering immediately. Finding one IDOR in your career pays for all the time you spent learning this chapter.

## ✅ Exercise

On [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) (run it locally — it's built for this):
1. Find one Broken Access Control issue (view another user's basket)
2. Land one XSS payload in the search or feedback field
3. Set up OWASP ZAP as a proxy and capture + modify one request in Repeater
4. Write each up using your [bug report template](templates/bug-report-template.md) with severity justified

**Next →** [Stage 6: Career Journey](07-career-journey.md) — or revisit [the full roadmap](README.md)
