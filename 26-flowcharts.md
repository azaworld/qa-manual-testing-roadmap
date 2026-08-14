# 🗺️ Scenario Flowcharts — Visualize & Teach Every QA Flow

> **Goal:** one animated, interactive flowchart for every core QA scenario — so you can *see* the flow, *remember* it, and *teach* it on camera without slides. The edges animate (flow), the diagrams recolor with the light/dark toggle, and many nodes are **clickable** — they open the real demo site to practice on. Each chart has a **🖥️ Teach with** (live site) and a **📖 Learn** (chapter) link.

> 💡 Every flowchart here is written in plain Mermaid text in the page source — you (or any contributor) can drop a ` ```mermaid ` block into *any* chapter and it renders the same way.

---

## 1. The tester's mindset — "how could this break?"
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://www.saucedemo.com/" target="_blank" rel="noopener">SauceDemo</a> (login <code>problem_user</code>) · 📖 <b>Learn:</b> <a href="01-foundations.html">Stage 0</a></div>

```mermaid
flowchart LR
  F["New feature"] --> Q{"How could this break?"}
  Q -->|empty| B1["Empty input"]
  Q -->|huge| B2["Huge / long input"]
  Q -->|twice| B3["Do it twice fast"]
  Q -->|midway| B4["Fail mid-flow"]
  Q -->|concurrent| B5["Two users at once"]
  B1 --> T["Turn each risk into a test"]
  B2 --> T
  B3 --> T
  B4 --> T
  B5 --> T
```

## 2. The Software Testing Life Cycle (STLC)
<div class="teachbox">📖 <b>Learn:</b> <a href="01-foundations.html">Stage 0</a></div>

```mermaid
flowchart LR
  A["Requirement analysis"] --> B["Test planning"] --> C["Case design"] --> D["Environment setup"] --> E["Execution"] --> F["Closure"]
  F -. "next sprint" .-> A
```

## 3. Choosing a test-design technique
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://demoqa.com/automation-practice-form" target="_blank" rel="noopener">DemoQA form</a> · 📖 <b>Learn:</b> <a href="02-test-design-techniques.html">Stage 1</a></div>

```mermaid
flowchart TD
  S{"What am I testing?"}
  S -->|"a range or limit"| BVA["Boundary Value + Equivalence Partitioning"]
  S -->|"combined rules"| DT["Decision Table"]
  S -->|"states & transitions"| ST["State Transition"]
  S -->|"many configs"| PW["Pairwise"]
  S -->|"something new / unknown"| EX["Exploratory charter"]
```

## 4. The defect lifecycle
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://github.com/azaworld/qa-roadmap/issues" target="_blank" rel="noopener">GitHub Issues</a> · 📖 <b>Learn:</b> <a href="05-agile-and-process.html">Stage 4</a></div>

```mermaid
flowchart LR
  N["New"] --> T["Triaged"] --> P["In Progress"] --> X["Fixed"] --> R{"Retest passes?"}
  R -->|yes| C["Closed ✅"]
  R -->|no| P
  T -->|"not a bug"| RJ["Rejected"]
  T -->|"fix later"| DF["Deferred"]
```

## 5. Severity vs Priority (the triage decision)
<div class="teachbox">📖 <b>Learn:</b> <a href="03-test-artifacts.html">Stage 2</a> · <a href="20-cheatsheets.html">Cheatsheet</a></div>

```mermaid
flowchart TD
  B["Bug found"] --> S{"Impact on user / business?"}
  S -->|high| HS["High severity"]
  S -->|low| LS["Low severity"]
  HS --> U{"Fix how urgently?"}
  LS --> U
  U -->|now| HP["High priority"]
  U -->|later| LP["Low priority"]
```

## 6. Writing a bug report that gets fixed
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://www.saucedemo.com/" target="_blank" rel="noopener">SauceDemo</a> + DevTools · 📖 <b>Learn:</b> <a href="03-test-artifacts.html">Stage 2</a></div>

```mermaid
flowchart LR
  A["Notice odd behavior"] --> B["Reproduce from a clean state"] --> C["Capture evidence: video, HAR, console"] --> D["Write: title, steps, expected vs actual, env"] --> E["Add severity + repro rate"] --> F["File in tracker"]
```

## 7. API test flow (four assertion layers)
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://petstore.swagger.io/" target="_blank" rel="noopener">Swagger Petstore</a> (click the node!) · 📖 <b>Learn:</b> <a href="13-api-testing-deep-dive.html">Stage 12</a></div>

```mermaid
flowchart TD
  A["Open Swagger Petstore"] --> B["Send a valid request"] --> C{"Status code correct?"}
  C -->|no| BUG["Log a bug"]
  C -->|yes| D["Check body: fields, types, values"] --> E["Check headers"] --> F["Send negatives: bad token, missing field, other user's id"] --> G["Verify side effect in DB / follow-up GET"]
  click A "https://petstore.swagger.io/" _blank
```

## 8. Should I automate this test?
<div class="teachbox">📖 <b>Learn:</b> <a href="09-path-to-automation.html">Stage 8</a> · <a href="15-automation-deep-dive.html">Stage 14</a></div>

```mermaid
flowchart TD
  Q{"Runs often + stable + high value?"}
  Q -->|yes| A["Automate it"]
  Q -->|"exploratory / one-off / changing UI"| M["Keep it manual"]
  A --> L{"At which level?"}
  L -->|logic| U["Unit test"]
  L -->|service| API["API test"]
  L -->|"critical journey"| E2E["E2E UI test"]
```

## 9. The CI/CD test pipeline
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://github.com/azaworld/qa-roadmap/actions" target="_blank" rel="noopener">GitHub Actions</a> · 📖 <b>Learn:</b> <a href="15-automation-deep-dive.html">Stage 14</a></div>

```mermaid
flowchart LR
  P["git push"] --> B["Build"] --> S["Smoke tests"] --> R{"Green?"}
  R -->|no| X["Block the merge"]
  R -->|yes| E["E2E + API tests"] --> G{"Gate: 0 critical bugs?"}
  G -->|no| X
  G -->|yes| D["Deploy 🚀"]
```

## 10. Choosing a performance test
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://test.k6.io/" target="_blank" rel="noopener">test.k6.io</a> · 📖 <b>Learn:</b> <a href="16-performance-testing.html">Stage 15</a></div>

```mermaid
flowchart TD
  Q{"What do I need to know?"}
  Q -->|"meets expected peak?"| L["Load test"]
  Q -->|"where does it break?"| S["Stress test"]
  Q -->|"survives a sudden surge?"| SP["Spike test"]
  Q -->|"degrades over time?"| SO["Soak test"]
```

## 11. Security — the IDOR test (Broken Access Control)
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://owasp.org/www-project-juice-shop/" target="_blank" rel="noopener">OWASP Juice Shop</a> · 📖 <b>Learn:</b> <a href="14-security-testing.html">Stage 13</a></div>

```mermaid
flowchart LR
  A["Log in as User A"] --> B["Note a resource id e.g. /orders/1001"] --> C["Log in as User B"] --> D["Request /orders/1001"] --> E{"Got A's data?"}
  E -->|yes| BUG["🚨 Critical: Broken Access Control"]
  E -->|"403 / 404"| OK["Secure ✅"]
```

## 12. AI + MCP agent testing loop
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://www.claude.com/product/claude-code" target="_blank" rel="noopener">Claude Code</a> + <a href="https://github.com/microsoft/playwright-mcp" target="_blank" rel="noopener">Playwright MCP</a> · 📖 <b>Learn:</b> <a href="12-ai-for-qa.html">Stage 11</a></div>

```mermaid
flowchart LR
  A["You: write a charter"] --> B["AI agent (via MCP)"] --> C["Drives a real browser"] --> D["Reads DOM, finds issues, drafts a test"] --> E["You review the assertions"] --> F{"Good enough?"}
  F -->|"refine"| A
  F -->|yes| G["Commit to CI"]
```

## 13. A structured exploratory session
<div class="teachbox">🖥️ <b>Teach with:</b> <a href="https://the-internet.herokuapp.com/" target="_blank" rel="noopener">the-internet</a> · 📖 <b>Learn:</b> <a href="02-test-design-techniques.html">Stage 1</a></div>

```mermaid
flowchart LR
  A["Charter: area + risk + time-box"] --> B["Recon (5 min): map it"] --> C["Attack: boundaries, negatives, interruptions"] --> D["Log findings live"] --> E["Report: bugs, coverage, open questions"]
```

## 14. The interview process, end to end
<div class="teachbox">📖 <b>Learn:</b> <a href="08-interview-prep.html">Stage 7</a> · <a href="19-interview-bank.html">Interview Bank</a></div>

```mermaid
flowchart LR
  A["Recruiter screen"] --> B["Technical round"] --> C["Practical task"] --> D["Behavioral (STAR)"] --> E["Panel / values"] --> O["Offer 🎉"]
```

---

> 🎓 Screen-share this page while teaching — walk a flowchart, then click through to its demo site and *do* it live. Full per-topic teaching scripts are in the [🎬 Teaching Kit](21-teaching-kit.html). Publish your videos on [AZADEMY](https://azademy.vercel.app/).

← Back to [the roadmap](README.md) · **See also:** [Teaching Kit](21-teaching-kit.html) · [Cheatsheets](20-cheatsheets.html)
