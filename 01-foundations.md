# Stage 0 — Foundations

> **Goal:** understand what QA actually is, how software gets built, and where testing fits — so everything later makes sense.

## 1. What QA actually is (and isn't)

| Term | What it means | Example |
|---|---|---|
| **Quality Assurance (QA)** | *Process-oriented.* Preventing defects by improving how software is built | Adding a review checklist before code merges |
| **Quality Control (QC)** | *Product-oriented.* Finding defects in the built product | Executing test cases on a release candidate |
| **Testing** | The activity of executing software to find defects | Clicking through checkout with an expired card |

**The mindset shift that makes you good:** developers ask *"how do I make this work?"* — testers ask *"how could this break?"* Your job is not to prove the software works. Your job is to **find the truth about its quality and communicate it clearly.**

## 2. The Seven Testing Principles (ISTQB — but explained like a human)

1. **Testing shows the presence of defects, not their absence** — you can never prove software is bug-free; you reduce risk.
2. **Exhaustive testing is impossible** — a 10-field form has millions of input combos. That's why test *design techniques* exist (Stage 1).
3. **Early testing saves money** — a requirement bug caught in review costs minutes; the same bug in production costs a rollback, support tickets, and trust.
4. **Defects cluster** — 80% of bugs live in 20% of modules. Find the hot spots (payment, auth, anything recently rewritten) and hit them hardest.
5. **The pesticide paradox** — re-running the same tests stops finding new bugs. Refresh and vary your tests.
6. **Testing is context-dependent** — you test a healthcare app differently than a game. (I tested payment systems at Mastercard — the tolerance for defects was effectively zero.)
7. **Absence-of-errors fallacy** — a bug-free product that solves the wrong problem is still a failure.

## 3. SDLC — how software gets built

**Software Development Life Cycle** phases (every model arranges these differently):

```
Requirements → Design → Development → Testing → Deployment → Maintenance
```

| Model | How it works | Where QA fits |
|---|---|---|
| **Waterfall** | Phases run once, in order | QA gets the product at the end (risky — bugs found late) |
| **Agile/Scrum** | 1–2 week sprints, ship increments | QA is embedded in the team, tests every sprint (this is your reality — see [Stage 4](05-agile-and-process.md)) |
| **V-Model** | Each dev phase has a matching test phase | Test design starts as soon as requirements exist |

## 4. STLC — the testing life cycle

**Software Testing Life Cycle** — what *you* do, phase by phase:

| Phase | Activity | Output |
|---|---|---|
| 1. Requirement analysis | Read the story/spec, ask questions, find ambiguity | Clarified requirements, testability notes |
| 2. Test planning | Decide scope, approach, people, schedule, risks | [Test plan](templates/test-plan-template.md) |
| 3. Test case design | Apply design techniques to write cases | [Test cases](templates/test-case-template.md), test data |
| 4. Environment setup | Get a stable place to test (staging, test accounts, data) | Ready environment |
| 5. Test execution | Run the cases, log defects, retest fixes | Execution results, [bug reports](templates/bug-report-template.md) |
| 6. Closure | Summarize: what was tested, what's still risky | Test summary report, go/no-go input |

**Real-world truth:** in agile these phases compress into days and overlap constantly. The order of *thinking* still holds.

## 5. Verification vs Validation

- **Verification** — *are we building the product right?* (reviews, walkthroughs, checking against spec)
- **Validation** — *are we building the right product?* (actually executing it, UAT)

## 6. The vocabulary that must be automatic

| Term | Meaning |
|---|---|
| **Error** | Human mistake in code or requirements |
| **Defect / Bug** | The flaw in the software caused by the error |
| **Failure** | The defect actually manifesting during execution |
| **Test case** | Preconditions + steps + expected result |
| **Test suite** | A collection of related test cases |
| **Test scenario** | A high-level thing to test ("verify checkout with expired card") |
| **Regression** | Re-testing existing features after changes |
| **Severity** | How bad the defect's impact is (set by QA) |
| **Priority** | How urgently it should be fixed (set with product) |

## ✅ Exercise

Take any app you use daily (e.g., a food delivery app). Write down:
1. Three ways it could *fail* that would be **critical severity**
2. Three defects that would be **low severity but high priority** (hint: a typo in the company name on the home page)
3. Which testing principle explains why the app still has bugs despite a QA team

**Next →** [Stage 1: Test Design Techniques](02-test-design-techniques.md)
