# Stage 2 — Test Artifacts That People Actually Use

> **Goal:** write the three documents that define your daily output — test plans, test cases, and bug reports — well enough that engineers and PMs act on them without asking follow-up questions.

## 1. The Test Plan — your strategy on one page

A test plan answers: **what are we testing, how, with what, by when, and what could go wrong.** In agile teams it's short — one page per feature/release beats a 40-page document nobody reads.

Core sections (full template: [templates/test-plan-template.md](templates/test-plan-template.md)):

| Section | The question it answers | Example |
|---|---|---|
| Scope — In | What WILL be tested | Checkout with card, PayPal; guest & member |
| Scope — Out | What will NOT (and why) | Gift cards (feature-flagged off this release) |
| Approach | How | EP/BVA on forms, exploratory on new flows, regression suite on payment |
| Environments | Where | staging.example.com, Chrome/Safari/Firefox latest, iPhone 15 + Pixel 8 |
| Test data | With what | Stripe test cards, seeded member accounts |
| Entry criteria | When testing starts | Build deployed, smoke passes, blockers from last round fixed |
| Exit criteria | When it's "done" | 100% critical cases run, no open critical/high defects |
| Risks | What could bite us | Payment sandbox flaky → book fallback window |

**Pro tip from real projects:** the *Out of scope* section prevents the worst release conversations ("wait, nobody tested gift cards?!"). Write it first.

## 2. Test Cases — precise, but not robotic

The template: [templates/test-case-template.md](templates/test-case-template.md). A strong case has:

- **ID** (`TC-CHK-004`), **Title** that says the *condition and expectation* — "Expired card is declined with a recoverable error message" beats "Test card payment 4"
- **Preconditions** — logged in? cart contents? feature flags?
- **Steps** — numbered, each with ONE action
- **Expected result per step** where it matters (not just at the end)
- **Priority** — P1 (run every build) → P3 (run before major releases)

### Anti-patterns (I reject these in reviews)

| ❌ Bad | ✅ Good | Why |
|---|---|---|
| "Check login works" | "Valid email + valid password lands on /dashboard within 3s" | Testable, unambiguous |
| 25 steps in one case | Split into cases per condition | One case = one verdict |
| Expected: "works correctly" | Expected: "Order status becomes *Confirmed*; confirmation email within 2 min" | "Correctly" isn't checkable |
| Hard-coded personal test data | Reference to shared seeded data | Anyone can run it |

See a real set: [examples/ecommerce-checkout-test-cases.md](examples/ecommerce-checkout-test-cases.md)

## 3. The Bug Report — your most-read writing

A developer should be able to reproduce your bug **without talking to you**. Full template: [templates/bug-report-template.md](templates/bug-report-template.md); real example: [examples/sample-bug-report.md](examples/sample-bug-report.md).

The non-negotiables:

1. **Title = symptom + condition**: "Checkout: double charge when Pay is double-clicked on slow connection" — findable in search six months later
2. **Steps to reproduce** — numbered, minimal, from a clean state
3. **Expected vs Actual** — two separate lines, no ambiguity
4. **Environment** — build/commit, browser + version, OS, account type, feature flags
5. **Evidence** — screenshot with the problem circled, or a 20-second video; HAR file / console log for anything network-y
6. **Severity + your reproduction rate** — "5/5 attempts" or "flaky, 2/5"

### Severity vs Priority (get this right in interviews AND in life)

| | High priority | Low priority |
|---|---|---|
| **High severity** | Payment charges twice | Crash in a legacy report 2 users open yearly |
| **Low severity** | CEO's name misspelled on homepage | Tooltip typo on settings page |

Severity = impact (QA owns it). Priority = order of fixing (product owns it, you advise).

## 4. RTM — Requirements Traceability Matrix

A simple grid mapping requirements → test cases → results, so you can answer "is REQ-12 tested?" instantly:

| Requirement | Test cases | Last run | Status |
|---|---|---|---|
| REQ-12 Guest checkout | TC-CHK-001..009 | 2026-08-10 | ✅ 9/9 pass |
| REQ-13 Saved cards | TC-CHK-010..014 | 2026-08-10 | ⚠️ 4/5 — BUG-2231 open |

In tools like TestRail/QASE this is automatic — but understand the concept, because "coverage" questions come up in every release meeting.

## 5. Test Summary Report — the closing argument

At the end of a cycle, one page: what was tested, pass/fail numbers, open defects with severity, what was NOT tested, and **your recommendation** (ship / ship with known issues / don't ship). This is where QA's voice matters most — write it plainly and stand behind it.

## ✅ Exercise

1. Copy the [bug report template](templates/bug-report-template.md) and write up a real bug from any app you use (every app has them)
2. Write 5 test cases for a login form using the template — include at least one negative case and one boundary case
3. Trade with a friend: can they execute your cases *without asking you anything*? That's the bar.

**Next →** [Stage 3: Types of Testing](04-types-of-testing.md)
