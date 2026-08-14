# 💬 QA Interview Questions — The Bank (Top 100+ with answers)

> **Goal:** the questions that actually get asked, with model answers and real examples — so you can walk in ready. Use it two ways: **study** it, or **teach/record** from it (each answer is a ready talking point, no slides needed). Pairs with [Stage 7: Interview Preparation](08-interview-prep.md) (strategy) — this page is the raw question bank.

**How to use:** start with the **Top 20 must-know** (full answers). Then drill the **category banks** (crisp answers). Finish with the **Mock Interview** protocol to rehearse out loud.

---

## 🥇 Top 20 must-know (full model answers)

**1. Severity vs Priority?**
Severity = technical impact; Priority = business urgency. *High severity / low priority:* a crash in a report 2 users open yearly. *Low severity / high priority:* the CEO's name misspelled on the homepage. QA sets severity; priority is agreed with product.

**2. Verification vs Validation?**
Verification = "are we building it right?" (reviews, static checks against spec). Validation = "are we building the right thing?" (executing it, UAT).

**3. Smoke vs Sanity vs Regression?**
Smoke = is the build stable enough to test at all (broad, shallow). Sanity = does this specific fix/area work (narrow, deep). Regression = did the change break anything that used to work.

**4. What is the STLC?**
Requirement analysis → test planning → test case design → environment setup → execution → closure. In agile it compresses and overlaps, but the thinking order holds.

**5. How would you test a login page?** *(structure, not a list)*
By dimension: functional (valid/invalid via EP), boundaries (password length), security (SQLi/XSS, lockout, HTTPS, masking), usability (error clarity, tab order), compatibility (browser matrix), state (already-logged-in, expired session, remember-me). Then prioritize by risk — auth is always high impact.

**6. Equivalence Partitioning & Boundary Value Analysis?**
EP: split inputs into groups that behave the same, test one per group. BVA: test on/around the edges (for 18–60, test 17/18/19 and 59/60/61) — where off-by-one bugs live.

**7. When do you stop testing?**
Against exit criteria, not "when it feels done": all P1 cases run, pass-rate threshold met, no open critical/high defects, coverage of requirements adequate, time/risk accepted by the business. I document what wasn't tested.

**8. A developer says "not a bug / works on my machine." What do you do?**
Re-check the requirement; if ambiguous, take it to the PM as a *requirements question*. For "works on my machine," diff environments (build, browser, data, flags) and attach a video + HAR so they see my exact reality. Most of these are environment/data differences.

**9. You find a critical bug an hour before release.**
Reproduce and pin the conditions + rate, gather evidence, escalate to the release owner immediately with impact in user terms, and present options (fix & retest / feature-flag off / ship with documented workaround). The decision is the business's; the evidence and the record are mine.

**10. Severity of a typo on the homepage?**
Usually low severity, but can be high *priority* (brand/legal). Great answer because it shows you separate the two axes.

**11. What makes a good bug report?**
Title = symptom + condition; minimal numbered repro from a clean state; expected vs actual as separate lines; environment (build, browser, OS, account, flags); evidence (screenshot/video/HAR/console); severity + reproduction rate. A dev should reproduce it without talking to me.

**12. Test case vs test scenario?**
Scenario = a high-level thing to test ("checkout with expired card"). Test case = the concrete steps + preconditions + expected result that verify it.

**13. What is a test plan?**
A one-page strategy: scope (in/out), approach, environments, test data, entry/exit criteria, risks, schedule. The *out-of-scope* section prevents the worst release conversations.

**14. How do you test an API without the UI?**
In Postman/curl: send valid requests, check status + body (fields/types/values) + response time; then attack — missing fields (400), bad token (401), someone else's resource id (403/404, not 200!), malformed JSON. Cross-check the API against the UI and the DB.

**15. Explain the test automation pyramid.**
Many fast unit tests at the base, fewer API/integration in the middle (QA sweet spot), few slow E2E/UI at the top. Push tests as far down as possible. The anti-pattern is the inverted pyramid — hundreds of brittle UI tests.

**16. What should you automate vs keep manual?**
Automate stable, repetitive, high-value checks (regression, smoke, data-driven, API). Keep manual: exploratory, usability, one-off, rapidly-changing UI, "does this look right?" judgment. ROI = runs saved × time − (build + maintenance).

**17. How do you handle flaky tests?**
Find the cause: hard sleeps → condition waits; shared-state races → isolate + fresh data; animation → wait for end state; ambiguous locators → tighten; network timing → mock/await. Retries are a stopgap, not a fix — a suite that only passes on retry is lying.

**18. Severity/priority of a security bug like IDOR?**
Broken Access Control is typically critical severity + highest priority — one user reading another's data is a breach. I'd reproduce privately, document impact, and escalate to security immediately.

**19. How do you test an AI/LLM feature?**
It's probabilistic, so I score rather than assert pass/fail: build an **eval set** (inputs + expected qualities), run it on every prompt/model change, and test for hallucination, bias, and prompt injection ("ignore previous instructions…"). Regression testing for prompts.

**20. Why QA / why should we hire you?**
I find the truth about quality and communicate it so the team can decide with eyes open. I think in risk, write artifacts engineers act on, and I've shipped real quality on payment, healthcare and e-commerce systems. *(Make it yours — use your story.)*

---

## 🧭 Manual & Fundamentals (bank)

| # | Question | Crisp answer |
|---|---|---|
| 21 | Error vs defect vs failure? | Error = human mistake; defect = the flaw it caused in the software; failure = the defect manifesting at run time |
| 22 | Positive vs negative testing? | Positive = valid inputs behave correctly; negative = invalid/unexpected inputs are handled gracefully |
| 23 | Decision table testing? | For combined business rules — one column per rule combo; exposes requirement gaps before you test |
| 24 | State transition testing? | For state machines (order, account) — test valid and invalid transitions (e.g., "locked" must not unlock on correct password) |
| 25 | Exploratory vs ad-hoc? | Exploratory is structured (charter + time-box + notes); ad-hoc is unstructured. Do exploratory |
| 26 | Retesting vs regression? | Retest = verify a specific fix with the exact failing steps; regression = check nothing else broke |
| 27 | What is a RTM? | Requirements Traceability Matrix — maps requirements → test cases → results, answers "is REQ-12 tested?" |
| 28 | Alpha vs beta testing? | Alpha = internal, pre-release; beta = real users, limited release, before GA |
| 29 | Static vs dynamic testing? | Static = no execution (reviews, walkthroughs); dynamic = executing the software |
| 30 | Defect clustering? | ~80% of defects live in ~20% of modules — focus there (payment, auth, recently changed code) |
| 31 | Pesticide paradox? | Re-running the same tests stops finding new bugs — refresh/vary them |
| 32 | Risk-based testing? | Prioritize by impact × likelihood; go deep where both are high, smoke-only where both are low |
| 33 | What's in a defect life cycle? | New → Triaged → In Progress → Fixed → Retest → Closed; branches: Rejected, Deferred, Reopened |
| 34 | Boundary of a text field with max 50 chars? | Test 49, 50, 51, plus empty and paste-over-limit — and confirm the server enforces it, not just the UI |
| 35 | How do you test with incomplete requirements? | Ask early, document assumptions, get them confirmed in writing, turn them into acceptance criteria |

## 🤖 Automation (bank)

| # | Question | Crisp answer |
|---|---|---|
| 36 | Page Object Model? | Separate page actions/locators from test assertions — UI change = fix one file, not fifty tests |
| 37 | Best locator strategy? | Role/label/text > test-id > CSS > (avoid) positional XPath |
| 38 | Why never use hard sleeps? | They're either too slow or still flaky — wait for a condition (visible/network idle/URL), which Playwright/Cypress do automatically |
| 39 | Data-driven testing? | Same test, many inputs from a data table — your EP/BVA table becomes the dataset |
| 40 | Playwright vs Selenium? | Playwright: auto-wait, multi-browser, trace viewer, parallel by default; Selenium: broadest language/browser support, older |
| 41 | How do you keep a suite fast? | Push tests down the pyramid, parallelize, mock externals, keep E2E to critical paths |
| 42 | What makes a test independent? | No shared state, any order, creates + cleans its own data, env-driven config |
| 43 | How do you run tests in CI? | On every push/PR (GitHub Actions), fail the build on failure, upload the report artifact |
| 44 | BDD / Cucumber — when? | When non-technical stakeholders need to read/own scenarios; overkill if only engineers use them |
| 45 | How do you report automation results? | HTML/Allure report with screenshots + video/trace on failure, visible to the whole team |

## 🔌 API & Data (bank)

| # | Question | Crisp answer |
|---|---|---|
| 46 | GET vs POST vs PUT vs PATCH? | Read / create / replace / partial-update — and test the API actually respects the semantics |
| 47 | Key status codes? | 200/201/204, 301/302, 400/401/403/404/409/422/429, 500/502/503 |
| 48 | 401 vs 403? | 401 = not authenticated (who are you?); 403 = authenticated but not allowed |
| 49 | Idempotency — why test it? | Same POST twice shouldn't create two orders — the classic double-charge bug |
| 50 | Contract testing? | Verify the implementation matches the OpenAPI spec (and consumers via Pact); half of API bugs live in that gap |
| 51 | REST vs GraphQL testing? | GraphQL: one endpoint, test field-level authz, deep-nesting DoS, introspection exposure |
| 52 | How do you test auth tokens? | Expired → 401, tampered → 401, user A's token on user B's resource → 403/404, decode JWT and check for leaked PII |
| 53 | Why use SQL in QA? | Confirm the UI action actually persisted, find duplicates, verify cross-table integrity |
| 54 | How to validate a JSON response? | Status + required fields present + correct types + correct values + schema validation |
| 55 | What is Newman? | Postman's CLI runner — turns your manual collection into CI automation |

## ⚡ Performance & 🔐 Security (bank)

| # | Question | Crisp answer |
|---|---|---|
| 56 | Load vs stress vs spike vs soak? | Expected peak / past breaking point / sudden surge / long duration |
| 57 | Why percentiles over averages? | An average of 200ms can hide a p99 of 8s — the tail is someone's every request |
| 58 | Key perf metrics? | Latency (p50/p95/p99), throughput (RPS), error rate, concurrency, saturation (CPU/mem/DB) |
| 59 | How do you find a bottleneck? | Watch server metrics (not just client): DB (indexes, N+1, pool), app, network, infra, third parties |
| 60 | What is a threshold in k6? | A pass/fail gate (e.g., `p(95)<500`) that fails the build on a perf regression |
| 61 | OWASP Top 10 — name a few? | Broken Access Control, Injection, Cryptographic Failures, Security Misconfig, Auth Failures |
| 62 | What is IDOR? | Insecure Direct Object Reference — change `/orders/1001` to `1002` and see someone else's data |
| 63 | Reflected vs stored XSS? | Reflected = echoed back in the response; stored = saved and served to other users |
| 64 | How do you test for SQL injection? | Inject `' OR '1'='1' --` and friends; watch for DB errors, changed results, timing differences |
| 65 | Client-side validation is enough? | Never — always test the server rejects tampered requests (bypass the UI in the proxy/Postman) |

## 🧠 AI × QA (bank — the 2026 edge)

| # | Question | Crisp answer |
|---|---|---|
| 66 | Will AI replace QA? | No — it replaces *re-checking*, not testing thinking. Judgment, risk and exploration matter more |
| 67 | What is an eval? | A scored test set for AI output (relevance/accuracy/tone) run on every prompt/model change |
| 68 | How do you test for hallucination? | Ground-truth eval set + LLM-as-judge + human spot-checks; measure factuality rate |
| 69 | What is prompt injection? | Malicious input that overrides instructions ("ignore previous…") — test your product's guardrails |
| 70 | What is MCP in testing? | Model Context Protocol — lets an AI agent drive a real browser (Playwright MCP) to explore and generate tests |
| 71 | How do you use AI day-to-day as QA? | Generate test ideas/data, draft bug reports, analyze logs — always verifying output; AI drafts, I decide |
| 72 | Risks of AI-generated tests? | Weak assertions ("page loaded"), false confidence — human review of assertions is the job |

## 🗣️ Behavioral (bank — prepare STAR stories)

| # | Question | What they're checking |
|---|---|---|
| 73 | Tell me about a bug you're proud of finding | Thinking, not luck — a bug that required a hypothesis |
| 74 | A conflict with a developer? | Diplomacy — end with the relationship intact |
| 75 | A release you recommended against? | Judgment + standing behind evidence |
| 76 | Too much to test, too little time? | Risk-based prioritization + communicating trade-offs |
| 77 | A bug that escaped to production? | Ownership + what you changed after (no blame) |
| 78 | How do you handle repetitive work? | Systems: checklists, rotation, and automating the boring parts |
| 79 | Disagree with your manager on quality? | Evidence + options, then respect the decision |
| 80 | How do you keep learning? | Concrete cadence (this roadmap, MoT, conferences, side projects) |

*(That's 80 core questions. Add the 20 answered at the top = 100. For 200+, each category's linked chapter and the resources below go deeper.)*

---

## 🎤 Mock Interview — rehearse out loud (like [educative.io/mock-interview](https://www.educative.io/mock-interview))

Reading answers ≠ saying them under pressure. Run this **30-minute self-mock** (record yourself — you'll reuse the footage):

1. **Rapid-fire (10 min):** answer 15 random questions from the banks above, out loud, 60–90s each. No notes.
2. **Deep-dive (10 min):** pick one — "test this login page" or "walk me through automating a checkout" — and talk through it structured, narrating your thinking.
3. **Practical (5 min):** open a [demo site](21-teaching-kit.md) and *do* a 5-minute exploratory session out loud (recon → attack → report).
4. **Behavioral (5 min):** answer 3 behavioral questions in STAR (Situation → Task → Action → Result).

**Free mock-interview platforms:** [Pramp](https://www.pramp.com/) · [interviewing.io](https://interviewing.io/) · [educative.io/mock-interview](https://www.educative.io/mock-interview) · a peer from [Ministry of Testing – The Club](https://club.ministryoftesting.com/).

> 🎓 Want a guided run-through with feedback? I cover mock interviews and question drills on **[AZADEMY](https://azademy.vercel.app/)**.

---

## 📚 More question sources (verified)

- [Ministry of Testing — interviews & community](https://www.ministryoftesting.com/)
- [Guru99 — Software Testing interview questions](https://www.guru99.com/software-testing-interview-questions.html)
- [Glassdoor — QA Engineer questions](https://www.glassdoor.com/) (search your target company)
- [Educative — testing courses & cheatsheets](https://www.educative.io/cheatsheets)

**Next →** practice on live sites in the [Teaching Kit & Demo Sites](21-teaching-kit.md) · or grab the [Cheatsheets](20-cheatsheets.md)
