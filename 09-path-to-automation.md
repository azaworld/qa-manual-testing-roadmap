# Stage 8 — The Path to Automation (without abandoning your craft)

> **Goal:** know when automation makes sense, what to learn first, and how to make the transition from a position of strength — as someone who already knows *what's worth testing*.

## First, the correct mental model

Automation doesn't replace testing — it replaces **re-checking**. A script verifies that known behavior still holds; a human explores, questions, and judges. The best automation engineers were good manual testers first, because **a fast suite of the wrong checks is worthless.** You already know what's worth checking. That's the hard part.

## When to automate (and when not to)

| Automate ✅ | Keep manual ❌ |
|---|---|
| Regression run every release | Anything run once or twice |
| Smoke suite on every build | Exploratory & usability testing |
| Data-driven repetition (same flow, 50 inputs) | Rapidly changing UI (you'll rewrite weekly) |
| API contract checks | Visual "does this look right?" judgment |
| Precise timing/race conditions humans can't hit | Edge cases needing human setup judgment |

ROI rule of thumb: `value = (manual runs saved × time per run) − (build cost + maintenance)`. Maintenance is the silent killer — flaky suites get ignored, and an ignored suite is worse than none.

## The learning path (in order — 3–6 months of evenings)

1. **API automation first, not UI.** Postman collections you already have → add test scripts → run via Newman. APIs change less than UIs, so your first suite won't demoralize you.
2. **One language: JavaScript/TypeScript or Python.** Variables, functions, loops, objects/dicts — you need less than you fear. Free: freeCodeCamp JS or Python basics.
3. **Playwright** (my recommendation, and what I run in production for client platforms) — modern, fast, auto-waits kill most flakiness that plagued Selenium. Their docs + codegen tool let you record-then-read real tests from day one. Learn Selenium *concepts* too — job listings still ask.
4. **Locators & the Page Object Model** — the difference between a suite that survives UI changes and one that dies.
5. **Git + CI basics** — push your tests, run them in GitHub Actions on schedule. "My tests run automatically every night" is a career-changing sentence.
6. **Reporting** — Allure or the built-in HTML reporter; results nobody sees don't exist.

Then, if the path pulls you: performance (k6), mobile (Appium), and AI-assisted testing (self-healing locators, AI test generation — this is where the industry is heading, and where I now spend my time via AZAI Labs).

## Your first real project (the portfolio version)

Automate the top 10 regression cases from your [manual portfolio project](07-career-journey.md):
1. A smoke suite in Playwright: login, core flow, checkout — running in GitHub Actions on every push
2. An API collection with negative cases, running via Newman in the same pipeline
3. README explaining *what you chose to automate and why* — that paragraph impresses more than the code

## The titles as you go

**Manual QA → QA Engineer (hybrid) → Automation Engineer / SDET → then everything opens up:** Senior SDET, QA Architect, DevOps-adjacent reliability roles (my Mastercard chapter — chaos engineering — grew from exactly this path), or leadership.

## The one warning

Don't become the person who automates *instead of* testing. The market is full of flaky-suite babysitters who lost the testing instinct. Your manual foundation — risk thinking, test design, bug intuition — is the moat. Automation is leverage on top of it, not a replacement for it.

---

**You've reached the end of the roadmap — but the journey compounds daily.** Star the repo, do the exercises, build the portfolio, and when you land the job or the promotion: [tell me](https://github.com/azaworld/qa-manual-testing-roadmap/issues). I mean it.

← Back to [the roadmap](README.md)
