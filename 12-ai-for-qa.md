# Stage 11 — AI × QA: The 2026 Playbook

> **Goal:** use AI as leverage on every QA activity, drive browsers with AI agents (MCP + Playwright), learn to test AI systems themselves — and position your career for the biggest shift QA has ever seen. This is where I spend my working life now (AZAI Labs: *build with agents, not headcount*), so this chapter is field notes, not theory.

## 1. The honest picture first

AI does not replace testing thinking — it **amplifies** it. Everything from Stages 0–2 (risk, test design, judgment) matters *more*, because AI produces volume and you must judge quality. The testers being displaced are the pure-execution ones; the testers being promoted are the ones directing AI.

## 2. How AI helps each QA activity you already do

| Your activity | How AI helps | How to prompt it |
|---|---|---|
| **Test case design** | Generates EP/BVA/negative cases you might miss; great at "what did I forget?" | Paste the requirement + your cases: *"Act as a senior QA. What conditions am I missing? Focus on boundaries, states, and concurrency."* |
| **Test data** | Generates realistic edge-case data instantly: unicode names, RTL text, boundary dates, malformed JSON | *"Generate 30 signup test records covering locale, length, and format edge cases, as CSV"* |
| **Bug reports** | Turns messy notes into a clean report in your [template](templates/bug-report-template.md) | Paste template + raw notes: *"Rewrite into this template. Flag missing info as TODO."* |
| **Exploratory charters** | Proposes attack ideas per feature type | *"Give me 10 exploratory charters for a file-upload feature, ranked by risk"* |
| **Requirement review** | Finds ambiguity before you test | *"List every ambiguous or untestable statement in this user story"* |
| **Log/HAR analysis** | Explains stack traces and network captures fast | Paste the trace: *"What's the likely root cause? What should I check next?"* |
| **Regression selection** | Suggests what to re-test from a diff/changelog | *"Given this changelog, which of these 40 test cases are most at risk?"* |

**The golden rule:** AI drafts, **you decide**. Never file a bug or sign off a release on AI output you didn't verify — you own the verdict ([Stage 2](03-test-artifacts.md) still applies, always).

## 3. MCP + Playwright — AI agents driving real browsers

<img src="assets/ai-mcp-flow.svg" alt="Animated AI agent testing loop: QA writes charter → AI agent via MCP → real browser → reads DOM → QA reviews, with a refine loop" width="100%" />

The biggest practical shift in automation: **[Playwright MCP](https://github.com/microsoft/playwright-mcp)** exposes a real browser to AI agents over the **Model Context Protocol (MCP)**. Any MCP-compatible client — Claude Code, Claude Desktop, Cursor — can open pages, click, type, read the DOM, and run tests.

### Why it works so well

- The agent reads the **accessibility tree** (ARIA snapshot), not screenshots — faster, deterministic, and cheap on tokens
- It drives Chromium, Firefox, and WebKit — real browsers, real behavior
- It sees Playwright's artifacts: traces, screenshots, network logs — so it can *debug*, not just execute

### The workflow that's winning in 2026 (and the one I run)

1. **Explore with the agent:** point an MCP-driven session at staging: *"Explore the checkout flow, try edge cases, report anything broken."* The agent walks the app like a junior tester with infinite patience.
2. **Generate candidate tests:** the agent emits Playwright test code from what it observed.
3. **Human review — this is the QA job now:** you check the assertions actually assert the right things (AI-generated tests love asserting "page loaded" and calling it coverage).
4. **Commit, run in CI, let the healer fix breakages:** Playwright's agentic loop (planner → generator → healer) proposes fixes when locators drift; you approve.

### Setup in Claude Code / Cursor (5 minutes)

```bash
# add the official Playwright MCP server
claude mcp add playwright -- npx @playwright/mcp@latest
```

Then literally ask: *"Open staging.example.com, add a product to the cart, and tell me if checkout works with an expired card."*

### Field warnings (the stuff blog posts skip)

- **Auth is the day-2 problem** — agents that re-login every run hit rate limits and trigger security alerts. Use storage-state files or dedicated test accounts with session reuse.
- **Shadow DOM hides elements** from naive automation; prefer accessibility-tree-based interaction (which MCP does) over CSS selectors.
- **Never point an agent at production** with write access. Staging, always. Treat agent runs like you'd treat a new hire's first week: supervised.

## 4. The AI-assisted QA tool landscape (2026)

| Category | Tools to know |
|---|---|
| Agentic browser testing | Playwright MCP + Claude Code/Cursor · Playwright test agents (planner/generator/healer) |
| Self-healing UI tests | Playwright healer · Testim · Mabl · Functionize |
| Visual AI | Applitools Eyes · Percy |
| AI test generation | GitHub Copilot for test code · Playwright codegen + AI review |
| Unit-test generation | Copilot · Claude Code (`/generate tests for this module`) |
| LLM eval frameworks | DeepEval · promptfoo · Langfuse · OpenAI Evals |

Don't chase all of them. Master **one agentic workflow** (MCP + Playwright) and **one eval framework** — that combination is rarer than knowing ten tools shallowly.

## 5. Testing AI systems — the new QA frontier

Every product is adding LLM features, and someone must answer *"is it good?"* That someone is QA. This is genuinely new work:

### What's different about testing AI

| Traditional software | LLM-powered software |
|---|---|
| Deterministic: same input → same output | Probabilistic: same input → *different* outputs |
| Pass/fail assertions | **Scored** evaluations (relevance, accuracy, tone) |
| Bugs are code defects | "Bugs" include hallucinations, bias, prompt injection |
| Test once per build | **Eval on every prompt/model change** — regression testing for prompts |

### The core practice: evals

An **eval** is a dataset of inputs + expected qualities, scored automatically (exact match, rubric scoring, or LLM-as-judge) on every change. Teams with great evals ship several times faster because they can *tell* whether a change helped. Start with [promptfoo](https://promptfoo.dev/) or [DeepEval](https://github.com/confident-ai/deepeval) — both free and approachable for QA people.

### AI security testing

Learn the **[OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)**: prompt injection, insecure output handling, data leakage, excessive agency. Manual attack practice: *"Ignore previous instructions and…"* variants against your own product's chatbot — you'll be shocked how often it works. (This pairs with [Stage 13: Security Testing](14-security-testing.md).)

## 6. Career in the AI era — where the market is going

From current market research (2026): companies report it's **harder to hire people who can evaluate AI than people who can build it** — and QA people are natural evaluators. Emerging roles:

| Role | What it is | Your path to it |
|---|---|---|
| **AI QA Engineer** | Owns quality for AI-powered products: evals, regression, agent testing | This chapter + Stage 8 automation base |
| **AI Evals Engineer** | Builds evaluation pipelines for LLM products — 2026's hottest new QA-adjacent discipline | Eval frameworks + data literacy |
| **LLM Auditor / AI Output Reviewer** | Reviews AI outputs for accuracy, bias, safety at scale | Deep manual-QA judgment + domain expertise |
| **Agentic automation engineer** | Designs and supervises AI agents that test (MCP workflows) | Playwright + MCP + prompt skill |

Compensation signal: AI-fluent QA roles are commanding a **substantial premium** over traditional QA at every level (US market reports show mid-level AI QA at roughly 1.5× traditional QA comp). The skills gap is your opportunity — most testers haven't started.

### Your 90-day AI upskill plan

1. **Weeks 1–2:** use AI daily for test design + bug reports (section 2) — build the prompt habit
2. **Weeks 3–4:** set up Playwright MCP, run your first agent-driven exploratory session on a practice site
3. **Weeks 5–8:** agent-generate a small test suite, review and harden it, run it in GitHub Actions
4. **Weeks 9–12:** build one eval set with promptfoo for any LLM feature (or a public chatbot), write up what you found
5. **Ship the proof:** all of it goes in your portfolio repo — *"supervised AI agents testing real software"* is a résumé line very few can write today

## ✅ Exercise

1. Take your Stage 1 password-reset test cases and ask an AI to find gaps — verify each suggestion before accepting it (notice how many are plausible but wrong: that judgment IS the job)
2. Install Playwright MCP and have an agent explore [saucedemo.com](https://www.saucedemo.com/); compare its bug list to yours
3. Write 5 prompt-injection attacks and try them on any public AI chatbot's guardrails

**Next →** [Stage 12: API Testing Deep Dive](13-api-testing-deep-dive.md)
