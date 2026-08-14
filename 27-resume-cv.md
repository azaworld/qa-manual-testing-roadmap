# 📄 QA Resume & CV — Junior → Mid → Senior → SDET (templates)

<style>
.resume-actions{display:flex;gap:10px;flex-wrap:wrap;margin:0 0 18px}.resume-actions a,.resume-actions button{border:1px solid var(--border);background:var(--bg-soft);color:var(--text);border-radius:9px;padding:8px 12px;font:inherit;font-weight:700;cursor:pointer;text-decoration:none}.resume-actions a:hover,.resume-actions button:hover{border-color:var(--accent);color:var(--accent)}
@media print{.topbar,.sidebar,.crumb,.complete-wrap,.pager,.foot,.resume-actions,.teachbox{display:none!important}.content{margin:0!important}.article{max-width:none!important;padding:0!important}.article a{color:#000!important;text-decoration:none!important}body{font-size:11pt!important}}
</style>

<div class="resume-actions">
  <a href="templates/qa-resume-cv-template.html">📋 Open copyable template</a>
  <button type="button" onclick="window.print()">🖨️ Print / save tutorial as PDF</button>
</div>

> **Goal:** write a resume that gets the interview — with **copy-paste templates for every level** and the exact rules recruiters and ATS bots screen for. This is a teachable tutorial: read the rules, copy the template for your level, swap in your own outcomes. Pairs with [Career Journey](07-career-journey.html) (portfolio) and [Interview Preparation](08-interview-prep.html) (the rounds).

<div class="teachbox">🎥 <b>Teaching this?</b> Screen-share a template, then rewrite one weak bullet into a strong one live (see the formula below). 📖 <b>Then:</b> <a href="08-interview-prep.html">Interview Prep</a></div>

**Copy-ready companion:** [open the QA Resume / CV master template](templates/qa-resume-cv-template.html). Learners can duplicate it while you teach.

## Tutorial plan — teach this without slides

| Lesson | Show on screen | Learner output |
|---|---|---|
| 1. Choose the target | One real QA/SDET job description | Target title + 12 true keywords |
| 2. Build the skeleton | [Master template](templates/qa-resume-cv-template.html) | ATS-safe first draft |
| 3. Rewrite bullets | Weak-vs-strong table below | Five measurable impact bullets |
| 4. Add proof | Learner's GitHub and CI report | Two linked portfolio projects |
| 5. Tailor with AI | Job description + resume in an LLM | Gap analysis—not fabricated skills |
| 6. Quality gate | Final checklist + PDF test | Application-ready PDF |

> **Teaching rule:** never tell learners to invent metrics, titles or tools. Use exact numbers when known; use honest scope (`5 portals`, `30+ cases`, `weekly releases`) when a percentage is unavailable.

---

## 1. The 7 rules of a QA resume that passes

1. **One page** for Junior/Mid; two pages max for Senior/SDET. Nobody reads three.
2. **Beat the ATS** (the bot that reads it first): use a simple single-column layout, standard section headings, no tables/images/columns for the parts that matter, and **mirror keywords from the job description** (e.g., "Playwright", "API testing", "CI/CD").
3. **Outcomes, not duties.** Every bullet = *what you did + how + the result*. Numbers win.
4. **Front-load impact.** Best bullet first under each role.
5. **Tailor per application.** Reorder skills/bullets to match the specific JD. 10 minutes; huge lift.
6. **Consistent + clean.** One font, consistent tense (past for old roles, present for current), no typos — a QA with typos is a contradiction.
7. **Link your proof.** GitHub portfolio, LinkedIn, live test repo — the [Playground](17-playground.html) artifacts.

---

## 2. The bullet formula (the whole game)

> **[Action verb] + [what you tested/built] + [tool/technique] + [result / metric]**

| ❌ Weak (duty) | ✅ Strong (outcome) |
|---|---|
| "Responsible for testing the website" | "Designed 120+ test cases (EP/BVA) for checkout; caught 14 pre-release defects including a double-charge bug" |
| "Did automation testing" | "Built a Playwright + TypeScript E2E suite (POM), cut regression time from 2 days to 25 min in CI" |
| "Worked with APIs" | "Automated 60+ API tests in Postman/Newman; found 3 auth flaws (IDOR) before release" |
| "Used JIRA" | "Ran defect triage in Jira; drove escape rate down 30% over 4 sprints" |

**No metric? Estimate honestly** ("~", "dozens of", "5-portal") or use scope ("across Chewy, Amazon, Walmart").

**Action verbs:** Designed · Built · Automated · Led · Reduced · Caught · Owned · Shipped · Architected · Mentored.

---

## 3. Sections (in order) & what goes in each

1. **Header** — Name · target title (e.g., "QA Automation Engineer") · city/remote · phone · email · LinkedIn · GitHub. *No photo, no DOB (for most markets).*
2. **Summary** — 2–3 lines: who you are + specialty + top achievement. (Template per level below.)
3. **Skills** — grouped, keyword-rich: Testing · Automation · API · Performance · Security · Languages · Tools · CI/CD. (ATS bank in §6.)
4. **Experience** — role, company, dates; 3–5 outcome bullets each.
5. **Projects / Portfolio** — *critical for juniors*: your public repos ([Playground](17-playground.html) artifacts) with links.
6. **Education & Certifications** — degree; ISTQB/Coursera if any.

---

## 4. Copy-paste templates by level

Copy the block for your level into Google Docs / [a builder](#5-free-tools--builders) and replace the bracketed parts.

### 🟢 Junior QA (0–2 yrs) — lead with skills + projects
```text
YOUR NAME
QA Engineer  |  Dhaka, Bangladesh (Open to remote)
+880-XXXX-XXXXXX  •  you@email.com  •  linkedin.com/in/you  •  github.com/you

SUMMARY
Detail-oriented QA engineer with a strong manual-testing foundation and hands-on
Playwright automation. Comfortable with test design (EP/BVA), API testing, and
bug reporting. Built a public test portfolio and eager to grow into automation.

SKILLS
Testing: Manual, functional, regression, exploratory, test case design (EP/BVA), UAT
Automation: Playwright, Selenium (basics)   API: Postman, REST
Tools: Jira, TestRail, Git, Chrome DevTools, SQL (basics)   Languages: JavaScript/TypeScript (basics)

PROJECTS
• QA Portfolio (github.com/you/qa-portfolio) — test plan, 40 test cases (EP/BVA),
  8 documented bugs for a demo e-commerce app (SauceDemo).
• Playwright E2E demo — 10 regression tests running in GitHub Actions on every push.
• Postman API suite — 30+ requests (CRUD + negatives) against restful-booker.

EXPERIENCE  (internship / freelance / part-time if any)
QA Intern — Company, City                                   Mon 20XX – Present
• Executed 200+ test cases per release; logged 30+ reproducible bug reports.
• Verified fixes and ran regression on the checkout module each sprint.

EDUCATION
B.Sc. in CSE — University Name, 20XX
Certifications: ISTQB Foundation (if any) · Test Automation University
```

### 🟡 Mid QA (2–4 yrs) — lead with impact
```text
YOUR NAME
QA Automation Engineer  |  City • Remote
phone • email • linkedin.com/in/you • github.com/you

SUMMARY
QA engineer with 3+ years across web and API testing, owning a feature area end to
end. Build and maintain Playwright/Selenium suites in CI and cut regression time
significantly. Strong on test strategy, API automation, and cross-team collaboration.

SKILLS
Testing: test strategy, risk-based testing, functional, regression, exploratory
Automation: Playwright (TS), Selenium, Page Object Model, data-driven
API: Postman, REST Assured, Newman, contract testing   Performance: k6 (basics)
CI/CD: GitHub Actions, Jenkins   DB: SQL   Tools: Jira, TestRail, Allure, Git

EXPERIENCE
QA Engineer — Company, City                                  20XX – Present
• Own quality for [feature/area]; set the test strategy and release gates.
• Built a Playwright (TS) E2E suite (POM, data-driven) in CI — regression 2 days → 30 min.
• Automated 70+ API tests (Postman/Newman); caught 5 auth/validation defects pre-release.
• Cut defect escape rate ~30% by adding smoke gates and risk-based prioritization.

QA Engineer — Previous Company                               20XX – 20XX
• [outcome] • [outcome] • [outcome]

EDUCATION / CERTIFICATIONS
B.Sc. CSE — University, 20XX  ·  ISTQB Foundation
```

### 🔴 Senior QA / QA Lead (4+ yrs) — lead with scope, risk & leadership
```text
YOUR NAME
Senior QA Engineer / QA Lead  |  City • Remote
phone • email • linkedin.com/in/you • github.com/you • portfolio-url

SUMMARY
Senior QA professional with 5+ years owning risk and quality strategy for
[domain, e.g. fintech/healthcare] at scale. Lead release readiness across
cross-functional teams, combine exploratory/API/automation coverage, and improve
quality metrics such as escape rate, cycle time and production incidents.

SKILLS
Quality leadership: strategy, risk analysis, release gates, metrics, hiring, mentoring
Automation: Playwright (TS), Selenium, CI regression, framework review
API & contract: Postman/Newman, REST Assured, Pact, GraphQL
Performance: k6, JMeter (load/stress/soak, percentile SLAs)
Security: OWASP Top 10, ZAP/Burp (release-gate checks)
CI/CD & cloud: GitHub Actions, Jenkins, Docker, AWS

EXPERIENCE
Senior QA Engineer / QA Lead — Company, City                 20XX – Present
• Led QA for [product] ([scale metric, e.g. 13M+ trips / 5 marketplace portals]);
  owned the go/no-go call and release gates.
• Built a risk-based test strategy across UI, API and data workflows, reducing
  release validation from [before] to [after].
• Cut defect escape rate from [X]% to [Y]%; mentored [N] junior/mid QAs.
• Partnered with Product, Engineering and Support to triage [scope] and prevent
  [business impact / production incident].

EDUCATION / CERTIFICATIONS
B.Sc. CSE — University  ·  ISTQB Advanced (if any)
```

### ⚙️ SDET / Automation Architect (4+ yrs) — lead with engineering depth
```text
YOUR NAME
Senior SDET / Test Automation Architect  |  City • Remote
phone • email • linkedin.com/in/you • github.com/you • portfolio-url

SUMMARY
Senior SDET with 5+ years designing test systems for web, API and distributed
services. Architect CI-integrated Playwright and contract-test frameworks,
improve reliability and observability, and use MCP/AI agents with human-reviewed
assertions to accelerate coverage without weakening quality gates.

SKILLS
Languages: TypeScript/JavaScript, Python or Java
Frameworks: Playwright, Selenium/Cypress, fixtures, POM, parallelization, sharding
API & contract: REST Assured/Postman, Pact, GraphQL, service virtualization
Performance/reliability: k6/JMeter, chaos testing, Prometheus/Grafana
Platform: GitHub Actions/Jenkins, Docker, AWS, test environments, secrets
AI-assisted QE: Playwright MCP, agent-generated tests, promptfoo/DeepEval, eval gates

EXPERIENCE
Senior SDET — Company, City                                  20XX – Present
• Architected a Playwright + TypeScript framework adopted by [N] contributors,
  reducing regression from [before] to [after] with parallel CI execution.
• Moved [X]% of brittle UI checks to API/contract layers, cutting flaky failures
  from [before] to [after] while preserving critical-path coverage.
• Added traces, videos, logs and failure classification, reducing mean time to
  diagnose failed builds by [X]%.
• Introduced supervised MCP/AI workflows for exploration and candidate-test
  generation; all assertions remained code-reviewed and deterministic in CI.
• Set engineering standards, reviewed automation PRs and mentored [N] engineers.

EDUCATION / CERTIFICATIONS
B.Sc. CSE — University  ·  ISTQB Advanced (if any)
```

---

## 5. Free tools & builders

- **[Reactive Resume](https://rxresu.me/)** — free, open-source, ATS-friendly, export PDF
- **[FlowCV](https://flowcv.com/)** — clean free templates
- **Google Docs** — search "resume" templates (simple, safe, ATS-readable)
- **[Overleaf](https://www.overleaf.com/)** — LaTeX (e.g. *Jake's Resume*) for a crisp one-pager
- **ATS check:** paste the JD + your resume into an LLM: *"Which keywords from this job description are missing from my resume?"*

### Safe AI workflow for tailoring

```text
You are reviewing my QA resume against the job description below.
1. Extract the 15 most important hard-skill and responsibility keywords.
2. Map each keyword to evidence already present in my resume.
3. Mark missing evidence as GAP — do not invent experience.
4. Suggest a clearer summary and reordered skills section.
5. Rewrite up to five bullets using only facts I provided.

[JOB DESCRIPTION]
[RESUME]
```

AI is the editor, not the author of your career history. You approve every claim.

## 6. ATS keyword bank (include the ones true for you)

`Manual testing` · `test case design` · `EP` · `BVA` · `exploratory` · `regression` · `smoke` · `UAT` · `defect lifecycle` · `Jira` · `TestRail` · `Playwright` · `Selenium` · `Cypress` · `Appium` · `Page Object Model` · `API testing` · `Postman` · `REST Assured` · `Newman` · `GraphQL` · `contract testing` · `SQL` · `k6` · `JMeter` · `performance testing` · `OWASP` · `security testing` · `CI/CD` · `GitHub Actions` · `Jenkins` · `Docker` · `JavaScript` · `TypeScript` · `Python` · `Java` · `Agile` · `Scrum` · `SDET` · `AI testing` · `MCP` · `LLM evals`

## 7. Cover letter & LinkedIn (short but worth it)

- **Cover note (3 lines):** why this company + your single strongest match + a link to proof. Skip generic paragraphs.
- **LinkedIn:** headline = target title + top skills (e.g., "QA Automation Engineer · Playwright · API · CI/CD"); About = your summary; feature your GitHub. Recruiters search here.

## 8. Common mistakes

- ❌ "Responsible for…" bullets (duties, not outcomes) · ❌ walls of text · ❌ listing every tool you've ever opened · ❌ fancy multi-column templates that ATS can't parse · ❌ no links to proof · ❌ one generic resume blasted everywhere · ❌ typos.

## ✅ Exercise
1. Copy your level's template; fill it with **your** outcomes using the §2 formula.
2. Rewrite 3 duty-bullets into outcome-bullets (add a number to each).
3. Paste a real QA job description + your resume into an LLM and ask which keywords you're missing; add the true ones.
4. Get one peer to read it in 20 seconds and tell you your top achievement — if they can't, front-load it.

**Next →** [Interview Preparation](08-interview-prep.html) · [Career Journey](07-career-journey.html) · [The Playground](17-playground.html) (build the portfolio your resume links to)
