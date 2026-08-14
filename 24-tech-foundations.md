# 🧱 Tech Foundations for QA — Coding, Databases, Algorithms & How Much AI

> **Goal:** answer the question every QA eventually asks — *"How much programming, database, algorithms, and AI do I actually need?"* The honest answer: **it depends on the role, and less than you fear for most of it.** This chapter scopes each skill by role so you learn exactly what you need and skip what you don't.

## The one-glance answer: how much of each, by role

| Skill | Manual QA | Automation / SDET | AI-QA specialist |
|---|:--:|:--:|:--:|
| **Programming** | 🟢 basics (read code) | 🔵 solid (write frameworks) | 🔵 solid |
| **SQL / Databases** | 🔵 solid (verify data) | 🔵 solid | 🔵 solid |
| **Algorithms & DS** | 🟢 light (concepts) | 🟡 moderate (write clean code) | 🟡 moderate |
| **Web/system basics** | 🔵 solid (HTTP, client-server) | 🔵 solid | 🔵 solid |
| **AI / LLM / MCP** | 🟢 basics (use AI daily) | 🟡 moderate (agents, evals) | 🔴 deep |

🟢 aware · 🟡 comfortable · 🔵 strong · 🔴 expert. **Don't over-invest** where a 🟢 is enough — spend that time on test design and risk instead.

---

## 1. 💻 Coding — how much & what

**Truth:** manual QA needs to *read* code and write light scripts; automation/SDET needs to *write maintainable* code. You need **far less** than a software engineer — no need to build compilers, just to automate checks and read the app.

### Pick ONE language
- **TypeScript / JavaScript** — pairs with Playwright & Cypress. *My recommendation for starting today.*
- **Python** — pairs with Playwright, Selenium, pytest, and AI/eval tooling.
- **Java** — enterprise Selenium + REST Assured shops.

### What you actually need to master (the 20% that covers 80%)
- [ ] Variables & data types (string, number, boolean, null/undefined)
- [ ] **Data structures:** arrays/lists and objects/dictionaries (the two you'll use constantly)
- [ ] Conditionals (`if/else`) and loops (`for`, `for…of`)
- [ ] **Functions** — arguments, return values, reuse
- [ ] `async/await` and promises (essential for UI/API automation)
- [ ] Reading errors & stack traces
- [ ] Basic OOP — classes/objects (enough for the [Page Object Model](15-automation-deep-dive.html))
- [ ] JSON — read and build it (APIs live on it)
- [ ] **Git** — clone, branch, commit, push, PR
- [ ] **CLI/terminal** — cd, ls, run scripts, env vars

You do **not** need (for QA): advanced memory management, building frameworks from scratch, design-pattern encyclopedias, or competitive-programming tricks.

**Learn it (free):** [freeCodeCamp](https://www.freecodecamp.org/learn) (JS/Python) · [The Odin Project](https://www.theodinproject.com/) · [Python for Everybody](https://www.py4e.com/) · [Learn Git Branching](https://learngitbranching.js.org/) · [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
**Prove it:** automate 8–10 cases in Playwright ([Stage 14](15-automation-deep-dive.html)).

---

## 2. 🗄️ Databases & SQL — how much & what

**Truth:** SQL is the highest-ROI technical skill for a manual tester. It lets you verify what the UI *claims* actually happened in the data — and it's asked in most QA interviews. Aim for **solid**, not DBA-level.

### What to master
- [ ] `SELECT … FROM … WHERE` with `AND/OR`, `LIKE`, `IN`, `BETWEEN`
- [ ] `ORDER BY`, `LIMIT`
- [ ] Aggregates: `COUNT`, `SUM`, `AVG`, `GROUP BY`, `HAVING`
- [ ] **JOINs** — INNER and LEFT (cross-table verification: paid orders missing invoices)
- [ ] Finding duplicates (`GROUP BY … HAVING COUNT(*) > 1`)
- [ ] Reading a schema (tables, columns, keys, relationships)
- [ ] NULL handling (`IS NULL`, and why `= NULL` fails)
- [ ] **Awareness:** transactions/ACID, indexes (why a query is slow), and that NoSQL (MongoDB) exists and is queried differently

### How QA uses it (the point)
The UI says the order is "shipped" — does the row agree? Did the action create exactly one record, or two (a double-submit bug)? See the [SQL cheatsheet](20-cheatsheets.html#-sql-for-qa-the-5-that-cover-90) for the 5 queries that cover 90% of QA needs.

> ⚠️ Read-only access on staging. **Never** run write/DELETE queries against real data.

**Learn it (free):** [SQLBolt](https://sqlbolt.com/) (interactive) · [Mode SQL Tutorial](https://mode.com/sql-tutorial/) · [PostgreSQL Exercises](https://pgexercises.com/) · practice at [DB Fiddle](https://www.db-fiddle.com/)

---

## 3. 🧮 Algorithms & Data Structures — how much (honestly)

**Truth:** most QA roles need **concepts and clean code**, not LeetCode grinding. You should understand the tools well enough to write non-terrible automation and to reason about performance — but you're not usually solving dynamic-programming puzzles. **Exception:** SDET roles at big tech companies *do* include DSA interview rounds — scope your prep to your target.

### What every QA should understand (light)
- [ ] **Arrays/lists vs hash maps/dictionaries** — and when to use each (lookup speed)
- [ ] **Big-O intuition** — "this loop inside a loop over N items is slow" (O(n²)); why hash-map lookup (O(1)) beats scanning a list (O(n)). You need the *instinct*, not the proofs.
- [ ] Linear vs binary search (sorted data), and that sorting has a cost
- [ ] Recursion — recognize it when you see it
- [ ] Sets (dedup), stacks/queues (concept)

### Where it actually shows up in QA
- Writing a data-driven test that isn't accidentally O(n²)
- Reasoning about **why** a feature is slow under load ([performance testing](16-performance-testing.html))
- Generating/deduping test data efficiently
- Passing the DSA round **if** you target an SDET role at a FAANG-tier company

**Learn it (free / by need):**
- Concepts for everyone: [Khan Academy — Algorithms](https://www.khanacademy.org/computing/computer-science/algorithms) · [Big-O cheat sheet](https://www.bigocheatsheet.com/)
- Only if your target role has a DSA round: [LeetCode](https://leetcode.com/) (start Easy, focus arrays/strings/hashmaps), [NeetCode roadmap](https://neetcode.io/roadmap)

> **Don't** spend six months on LeetCode "to be safe." Most QA offers never test it. Confirm the interview format first (ask the recruiter — see [Stage 7](08-interview-prep.html)).

---

## 4. 🌐 Web & system fundamentals (the quiet essentials)

Every tester is better for knowing how the thing they test actually works:

- [ ] **HTTP** — methods, status codes, headers, request/response ([cheatsheet](20-cheatsheets.html#-http-status-codes))
- [ ] **Client–server model** — what runs in the browser vs on the server
- [ ] **APIs** — REST & a little GraphQL ([Stage 12](13-api-testing-deep-dive.html))
- [ ] **Browser basics** — DOM, DevTools (Network/Console), cookies/localStorage
- [ ] **CI/CD** — what a pipeline is; running tests on every push (GitHub Actions)
- [ ] **Linux/CLI** — navigate, run commands, tail logs
- [ ] **Networking awareness** — DNS, HTTPS/TLS, latency, caching

**Learn it (free):** [MDN Web Docs](https://developer.mozilla.org/) · [HTTP overview (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [Roadmap.sh — QA](https://roadmap.sh/qa)

---

## 5. 🤖 How much AI do you need?

AI fluency is now a core QA skill, but "how much" scales with your ambition:

| Level | Who | What to know |
|---|---|---|
| 🟢 **Baseline (every QA)** | all testers, today | Use AI daily for test design, data, bug reports, log triage — *verifying every output*. Prompt basics. → [Stage 16 §4](22-ai-powered-qa.html) |
| 🟡 **Practitioner (automation/SDET)** | most modern roles | Drive browsers with MCP + Playwright agents; review generated tests; basic evals. → [Stage 11](12-ai-for-qa.html) |
| 🔴 **Specialist (AI-QA / evals)** | AI-product teams | Build eval pipelines, red-team LLMs, test agentic systems, own the AI quality bar. → [Stage 16](22-ai-powered-qa.html) + [Tools Directory](23-ai-tools.html) |

**The prerequisite that never changes:** you must be a good tester *first* — AI amplifies judgment; it doesn't replace it. Master [test design](02-test-design-techniques.html) and [risk](05-agile-and-process.html) before leaning on AI. Full detail + a readiness check: [Stage 16 §2](22-ai-powered-qa.html#2--before-you-implement-ai--what-qa-must-know-first).

---

## 6. 🗺️ A sane learning order

1. **Web/system basics + HTTP** — understand the thing you test
2. **SQL** — highest ROI; verify data, ace interviews
3. **One language (basics)** — read code, write light scripts
4. **Git + CLI** — the developer workflow
5. **Automation** — apply the language ([Stage 14](15-automation-deep-dive.html))
6. **Algorithms (light)** — enough for clean code + performance intuition
7. **AI baseline → practitioner** — layer it on a solid testing foundation

Don't wait to "finish" one before starting the next — learn just enough to move, then deepen as real work demands.

## ✅ Exercise

1. Do the first 5 [SQLBolt](https://sqlbolt.com/) lessons — then write the 5 QA queries from the [cheatsheet](20-cheatsheets.html#-sql-for-qa-the-5-that-cover-90) from memory.
2. Write one JavaScript/Python function that takes an array of orders and returns the count per status (hint: use a hash map/dictionary — that's your DSA intuition in action).
3. Check your target job description: does it list a coding/DSA round? Scope your prep to the answer.

> 🎓 Guided, hands-on versions of all of this — programming, SQL, and AI — are tracks on **[AZADEMY](https://azademy.vercel.app/)**.

**Next →** [Stage 8: Path to Automation](09-path-to-automation.html) · [Stage 12: API Testing](13-api-testing-deep-dive.html) · [Stage 16: AI-Powered QA](22-ai-powered-qa.html)
