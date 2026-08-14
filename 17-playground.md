# 🎮 The Playground — Practice on Real Apps

> **Goal:** stop reading, start doing. These are safe, legal, deliberately-testable apps. Each one comes with a **mission** and a **win condition** — complete them and you'll have real artifacts for your portfolio. Testing is a skill; skills need reps.

> ⚠️ **Rule of the arena:** only test the apps listed here (or your own). They're built for practice. Never point tools at systems you don't own or aren't authorized to test.

## 🥉 Missions — Manual & Functional

### Mission 1 — Break the checkout
**App:** [SauceDemo](https://www.saucedemo.com/) (a full mock store; try the `locked_out_user` and `problem_user` logins too)
**Mission:** design and run a checkout test suite using [EP/BVA](02-test-design-techniques.md). Try the different user types — one of them has deliberately broken behavior.
**Win:** 15+ test cases in your [template](templates/test-case-template.md), and at least 3 written-up bugs.

### Mission 2 — The tricky-widget hunt
**App:** [the-internet](https://the-internet.herokuapp.com/) (every hard UI element: iframes, dynamic loads, file uploads, auth)
**Mission:** write exploratory [charters](02-test-design-techniques.md#7-exploratory-testing--structured-not-random) for 5 of the trickiest pages. Time-box 30 min each.
**Win:** session notes documenting what you tried and what surprised you.

### Mission 3 — Full signup-to-order journey
**App:** [Automation Exercise](https://automationexercise.com/)
**Mission:** run one complete E2E journey (register → browse → cart → checkout) and one negative pass (invalid data at every step).
**Win:** an [E2E test case set](examples/ecommerce-checkout-test-cases.md) + a bug journal.

## 🔌 Missions — API

### Mission 4 — CRUD and destroy
**App:** [restful-booker](https://restful-booker.herokuapp.com/apidoc/index.html) (deliberately buggy booking API)
**Mission:** in Postman, test create → read → update → delete asserting all [four layers](13-api-testing-deep-dive.md#2-designing-api-test-cases-same-craft-new-surface) (status, body, headers, side effects). Attack auth with expired/invalid tokens.
**Win:** a runnable Postman collection (40+ requests, negatives included) + a README of the bugs you found.

### Mission 5 — The contract check
**App:** [ReqRes](https://reqres.in/) / [GoRest](https://gorest.co.in/)
**Mission:** validate responses against their schema; find one place where reality doesn't match the docs.
**Win:** a documented contract-vs-reality gap.

## 🔐 Missions — Security *(learn the OWASP mindset first: [Stage 13](14-security-testing.md))*

### Mission 6 — Steal your own basket
**App:** [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) (run locally — built for this)
**Mission:** find one **Broken Access Control** issue (view another user's data) and land one **XSS** payload.
**Win:** two security bugs written up with severity justified — and set up [OWASP ZAP](https://www.zaproxy.org/) as a proxy to capture + modify one request.

### Mission 7 — The vulnerable API
**App:** [OWASP crAPI](https://github.com/OWASP/crAPI)
**Mission:** find one API authorization flaw (BOLA/IDOR at the API level).
**Win:** a reproduction with the exact requests.

## ⚡ Missions — Performance *(method: [Stage 15](16-performance-testing.md))*

### Mission 8 — Find the knee
**App:** [test.k6.io](https://test.k6.io/) (safe to load-test)
**Mission:** write a k6 load test (ramp → hold → down) with a `p(95)<800` threshold and think-time. Then turn it into a spike test.
**Win:** a report with p50/p95/p99, throughput, error rate, and the load level where it starts to bend.

## 🤖 Missions — Automation & AI *(build: [Stage 14](15-automation-deep-dive.md) · agents: [Stage 11](12-ai-for-qa.md))*

### Mission 9 — Your first green pipeline
**App:** [SauceDemo](https://www.saucedemo.com/)
**Mission:** automate 8–10 regression cases in Playwright (POM, data-driven), running in GitHub Actions on every push.
**Win:** a public repo with a green CI badge and an HTML report artifact.

### Mission 10 — Let an agent explore
**App:** any practice app above
**Mission:** set up [Playwright MCP](12-ai-for-qa.md#3-mcp--playwright--ai-agents-driving-real-browsers) and have an AI agent explore it; compare its bug list to yours.
**Win:** a write-up of what the agent caught, what it missed, and which of its generated assertions you'd actually keep.

---

## 🏆 The meta-mission

Complete missions across at least **four** categories and you'll have a portfolio that beats any certificate: manual test cases, bug reports, a Postman collection, a security finding, a k6 report, and a green automation pipeline. That's not a "learner" — that's a **hire**.

> 💬 Finished a mission? [Share it in an issue](https://github.com/azaworld/qa-roadmap/issues) — I feature great ones.

← Back to [the roadmap](README.md)
