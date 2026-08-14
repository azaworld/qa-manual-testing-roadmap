# 🤖 The AI QA Tools Directory (prioritized & auto-updated)

> **Goal:** every AI tool a QA should know — **what it is, why it matters, how it works, and what to do to start** — ranked by priority so you don't miss anything. Pairs with [Stage 16: AI-Powered QA](22-ai-powered-qa.html) (the strategy) and [Stage 11: AI × QA](12-ai-for-qa.html) (hands-on).

> 🔄 **This page auto-updates.** The latest versions of the open-source tools below are refreshed weekly by a [GitHub Action](https://github.com/azaworld/qa-roadmap/actions) — **last refreshed: {{ site.data.tool_versions.updated }}.** (See "How the auto-update works" at the bottom.)

**Priority legend:** 🥇 **learn first** (high-leverage, mostly free) · 🥈 **strong / next** · 🥉 **situational / enterprise**.

---

## ⭐ Start here — the 5 to learn first

If you do nothing else, learn these — they're free or accessible and cover 80% of the value:

1. **[Claude Code](https://www.claude.com/product/claude-code)** or **[Cursor](https://cursor.com/)** — your AI cockpit (runs agents, MCP, generates & reviews tests)
2. **Playwright MCP** `{{ site.data.tool_versions.tools.playwright-mcp.version }}` — lets the agent drive a real browser
3. **Playwright + Test Agents** `{{ site.data.tool_versions.tools.playwright.version }}` — the automation engine, with planner/generator/**healer**
4. **promptfoo** `{{ site.data.tool_versions.tools.promptfoo.version }}` — evals + red-teaming for AI features
5. **GitHub Copilot** — inline test generation in your editor

---

## 1. 🥇 AI cockpit & agentic browser control (the foundation)

The layer everything else plugs into: an AI client + MCP + a browser engine.

| Tool | Tier | What & why | How it works | Get started |
|---|---|---|---|---|
| [Claude Code](https://www.claude.com/product/claude-code) | 🥇 | Terminal-native AI agent; runs MCP servers, drives tests, reviews code | You prompt; it plans, edits, runs, and calls tools | `npm i -g @anthropic-ai/claude-code`, then `claude` |
| [Cursor](https://cursor.com/) | 🥇 | AI-first IDE; great for generating & refactoring test code | Chat + inline edits + MCP support | Install, open your test repo, enable MCP |
| **Playwright MCP** `{{ site.data.tool_versions.tools.playwright-mcp.version }}` | 🥇 | Exposes a real browser to any AI agent via [MCP](https://modelcontextprotocol.io/) — the key primitive | Agent reads the accessibility tree, clicks/types, runs tests | `claude mcp add playwright -- npx @playwright/mcp@latest` |
| [ChatGPT](https://chat.openai.com/) / [Claude](https://claude.ai/) (web) | 🥇 | Test-design, data, bug-report drafting, log triage | Prompt with role + context + constraints | Free tiers; see the [prompt library](22-ai-powered-qa.html#7--prompt-patterns-for-qa-copy-paste-library) |

## 2. 🥇 Automation engine with built-in AI

| Tool | Tier | What & why | How it works | Get started |
|---|---|---|---|---|
| **Playwright + Test Agents** `{{ site.data.tool_versions.tools.playwright.version }}` | 🥇 | Open-source E2E with first-party **planner → generator → healer** agents; free | Agents author and auto-repair tests in plain Playwright code | [playwright.dev](https://playwright.dev/) · `npm init playwright@latest` |
| [Playwright Codegen](https://playwright.dev/docs/codegen) | 🥇 | Record clicks → test code (then you harden it) | Records actions into a spec | `npx playwright codegen <url>` |

## 3. 🥈 Autonomous / natural-language test platforms (commercial)

Write tests in plain English or from recordings; AI builds and maintains them. Great for teams; most are paid with trials/demos.

| Tool | Tier | What & why | How it works |
|---|---|---|---|
| [Mabl](https://www.mabl.com/) | 🥈 | AI-native, low-code; agentic tester builds E2E from user stories | NL/record → adaptive healing + computer vision |
| [testRigor](https://testrigor.com/) | 🥈 | Plain-English test authoring, very low maintenance | Executable specs in English |
| [Tricentis Testim / AI Workspace](https://www.tricentis.com/products/ai-workspace) | 🥈🥉 | Codeless authoring + self-healing; 2026 agentic "AI Workspace" (test creation/automation/perf agents) | AI locators, auto-heal, agentic execution |
| [Functionize](https://www.functionize.com/) | 🥉 | ML-driven enterprise testing; NL test creation | Specialized agents + ML models |
| [Katalon](https://katalon.com/) | 🥈 | Broad platform (web/API/mobile) for mixed-skill teams | Low-code + AI assists |
| [QA Wolf](https://www.qawolf.com/) | 🥈 | Fully-managed coverage (they write & maintain your tests) | Service + Playwright under the hood |
| [ACCELQ](https://www.accelq.com/) | 🥉 | Codeless cross-platform, enterprise | AI-assisted, business-process focused |
| [LambdaTest KaneAI](https://www.lambdatest.com/kane-ai) | 🥈 | NL test authoring on a real device/browser cloud | AI agent + cloud grid |
| [BrowserStack Low Code](https://www.browserstack.com/low-code-automation) | 🥈 | NL authoring + self-healing on real devices | Low-code + device cloud |
| [Shiplight](https://www.shiplight.ai/) | 🥈 | AI-coding-agent workflow; YAML tests in git, heals as reviewable PRs; on Playwright | Intent re-derivation + cached locators |
| [Rainforest QA](https://www.rainforestqa.com/) | 🥉 | No-code with AI test generation | Visual authoring |

## 4. 🩹 Self-healing (reduce locator maintenance)

Overlaps with above — the key mechanism to know. **[Playwright healer](https://playwright.dev/docs/test-agents)** (free, 🥇), plus [Testim](https://www.testim.io/), [Mabl](https://www.mabl.com/), [Functionize](https://www.functionize.com/), [Shiplight](https://www.shiplight.ai/). *Rule: healing is a suggestion — you approve the fix.*

## 5. 👁️ Visual AI testing

| Tool | Tier | What & why | How it works |
|---|---|---|---|
| [Applitools](https://applitools.com/) | 🥈 | Leading Visual AI; "eye-like" diffing that ignores noise | Visual AI baselines + smart diff ($$$) |
| [Percy (BrowserStack)](https://percy.io/) | 🥈 | Visual regression in CI | Snapshot + diff |
| [Meticulous](https://www.meticulous.ai/) | 🥉 | Auto-generates visual/functional tests from real usage | Records sessions, replays |

## 6. 🧑‍💻 AI test / unit-code generation (dev-side)

| Tool | Tier | What & why | How it works | Get started |
|---|---|---|---|---|
| [GitHub Copilot](https://github.com/features/copilot) | 🥇 | Inline test scaffolding across languages; dedicated "tests" agent | Prompt/inline in editor | Editor extension |
| [Qodo (CodiumAI)](https://www.qodo.ai/) | 🥈 | Behavior-first, context-aware tests tied to PRs | Analyzes intent, generates + reviews | IDE plugin |
| [Diffblue Cover](https://www.diffblue.com/) | 🥉 | Autonomous JUnit generation for enterprise **Java** at scale | Reinforcement-learning search | CLI/IDE |
| [Amazon Q Developer](https://aws.amazon.com/q/developer/) | 🥈 | Test scaffolding in AWS-centric stacks | Inline suggestions | Editor extension |

## 7. 🧠 Testing AI systems — LLM evals & red-team (the 2026 edge)

If your product has AI features, this is your job. Start with promptfoo + DeepEval.

| Tool | Tier | What & why | How it works | Get started |
|---|---|---|---|---|
| **promptfoo** `{{ site.data.tool_versions.tools.promptfoo.version }}` | 🥇 | Evals + **red-teaming/security**; compare models, harden prompts; most-adopted OSS | YAML config, CLI, CI-friendly | `npx promptfoo@latest init` |
| **DeepEval** `{{ site.data.tool_versions.tools.deepeval.version }}` | 🥇 | "PyTest for LLMs" — unit-test-style evals | Python assertions on LLM output | `pip install deepeval` |
| **RAGAS** `{{ site.data.tool_versions.tools.ragas.version }}` | 🥈 | Reference-free RAG metrics (faithfulness, relevancy, context) | Metrics library | `pip install ragas` |
| **Langfuse** `{{ site.data.tool_versions.tools.langfuse.version }}` | 🥈 | Self-hostable tracing + evals + dashboards | Observability SDK | [langfuse.com](https://langfuse.com/) |
| **Arize Phoenix** `{{ site.data.tool_versions.tools.phoenix.version }}` | 🥈 | OpenTelemetry-native, self-hostable eval/tracing | Traces + evals | `pip install arize-phoenix` |
| **OpenAI Evals** `{{ site.data.tool_versions.tools.openai-evals.version }}` | 🥉 | Reference eval framework + registry | Python eval specs | [github.com/openai/evals](https://github.com/openai/evals) |
| [Braintrust](https://www.braintrust.dev/) / [LangSmith](https://www.langchain.com/langsmith) | 🥈 | Hosted eval platforms: human annotation, regression tracking, dashboards | SaaS | free tiers |

**AI security:** [OWASP Top 10 for LLM Apps](https://owasp.org/www-project-top-10-for-large-language-model-applications/) (the checklist) · [garak](https://github.com/NVIDIA/garak) (LLM vuln scanner) · promptfoo red-team (prompt-injection).

## 8. 📚 The living list (bookmark it)

- **[awesome-ai-testing](https://github.com/tugkanboz/awesome-ai-testing)** — a community-curated, continuously-updated list of AI testing tools (test generation, self-healing, MCP, LLM eval). The best single place to catch new entrants.

---

## 🧭 How to choose (decision guide)

- **Solo / open-source / want control?** → Claude Code or Cursor + Playwright MCP + Playwright Test Agents. (All free.)
- **Team wants low-code + managed healing?** → Mabl, testRigor, or Tricentis.
- **Don't want to write/maintain tests at all?** → QA Wolf (managed) or Rainforest.
- **Enterprise Java legacy?** → Diffblue Cover for unit tests.
- **Heavy visual UI?** → Applitools or Percy.
- **Your product has LLM/AI features?** → promptfoo + DeepEval (add Langfuse/Phoenix for tracing).
- **Just want faster daily QA?** → an AI client + the [prompt library](22-ai-powered-qa.html#7--prompt-patterns-for-qa-copy-paste-library).

> **Don't buy ten tools.** Master one agentic workflow (MCP + Playwright) and one eval tool (promptfoo). Depth beats breadth.

---

## 🔄 How the auto-update works

You asked for a system that stays current with releases — here it is, living in the repo:

1. **`_data/tool_versions.yml`** holds the latest version of each tracked open-source tool.
2. **[`.github/workflows/update-tool-versions.yml`](https://github.com/azaworld/qa-roadmap/blob/main/.github/workflows/update-tool-versions.yml)** runs **every Monday** (and on-demand from the Actions tab). It queries each tool's GitHub Releases API, rewrites the data file, and commits only if a version changed — which triggers a site rebuild.
3. This page renders those versions live, so the badges above are always current — **last refreshed {{ site.data.tool_versions.updated }}**.

**To add a tool to the tracker:** add its `key|owner/repo` line to the workflow's `tools` list. **To run it now:** open the repo's **Actions → "Update AI-QA tool versions" → Run workflow**.

> 🎓 Learn to actually *use* these in guided courses on **[AZADEMY](https://azademy.vercel.app/)**.

---

**Sources (2026):** [awesome-ai-testing](https://github.com/tugkanboz/awesome-ai-testing) · [QA Wolf — 12 best AI testing tools](https://www.qawolf.com/blog/the-12-best-ai-testing-tools-in-2026) · [Shiplight — best AI QA tools](https://www.shiplight.ai/blog/best-ai-qa-tools-2026) · [TestDino — Playwright AI ecosystem](https://testdino.com/blog/playwright-ai-ecosystem) · [DeepEval — top eval frameworks](https://deepeval.com/blog/top-5-llm-evaluation-frameworks) · [Braintrust — DeepEval alternatives](https://www.braintrust.dev/articles/deepeval-alternatives-2026)

← Back to [the roadmap](README.md) · **See also:** [Stage 16: AI-Powered QA](22-ai-powered-qa.html) · [Cheatsheets](20-cheatsheets.html)
