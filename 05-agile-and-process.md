# Stage 4 — QA in Agile Teams

> **Goal:** operate inside a real sprint — where testing is continuous, requirements are conversations, and you are the team's risk radar.

## 1. Your week in a Scrum team

| Ceremony | Your job there |
|---|---|
| **Backlog refinement** | The highest-leverage hour of your week. Ask the questions that become bugs later: "What happens if the coupon expires mid-checkout?" Push for **testable acceptance criteria** |
| **Sprint planning** | Estimate testing effort *with* dev estimates, flag test-data/environment needs early |
| **Daily standup** | Surface blockers fast ("staging is down, 6 cases blocked") and *risk*, not just status |
| **Review/demo** | You often demo — you know the edge cases that impress stakeholders |
| **Retro** | Bring data: "8 of 12 bugs this sprint were requirement gaps — let's fix refinement" |

## 2. The Definition of Done includes QA

A story is NOT done when the code is merged. A healthy DoD:

- [ ] Acceptance criteria verified on staging
- [ ] Negative & boundary cases executed
- [ ] Regression on touched areas passed
- [ ] No open critical/high defects
- [ ] Test cases updated in the suite

Fight for this in writing. "Done in dev" ≠ done.

## 3. The defect lifecycle

```
New → Triaged → In Progress → Fixed → Ready for Retest → Retested ─→ Closed
         │                                       │
         ├→ Rejected (not a bug / by design)     └→ Reopened (fix failed) → In Progress
         └→ Deferred (valid, fix later — needs a ticket + owner, or it's a lie)
```

**Triage** is where severity meets business priority. Come prepared: reproduction rate, affected user %, workaround exists or not. You're the evidence, product is the judge.

## 4. Entry & exit criteria — release gates

I run releases with explicit gates (this saved the FUR4 5-portal program more than once):

**Entry (testing starts):** build deployed to staging · smoke suite green · previous blockers verified · test data seeded
**Exit (we can ship):** 100% of P1 cases executed · ≥95% pass rate overall · zero open critical/high · known issues documented & signed off by product

No gate, no discipline — "we'll test it in prod" becomes the process.

## 5. QA metrics that actually matter

| Metric | Formula | What it tells you |
|---|---|---|
| **Defect escape rate** | prod bugs ÷ (prod + pre-release bugs) | Is your net catching things? The single most honest QA metric |
| **Defect density by module** | bugs per feature/module | Where to focus next cycle (defect clustering!) |
| **Requirement-gap ratio** | bugs traced to unclear requirements | Ammunition to improve refinement |
| **Test execution progress** | cases run ÷ planned, daily | Burndown for the release conversation |
| **Reopen rate** | reopened ÷ fixed | Fix quality / repro quality signal |

Avoid vanity metrics: raw bug counts and "number of test cases written" reward the wrong behavior.

## 6. Risk-based testing — the senior skill

You never have time to test everything. Score each area **Impact × Likelihood** (1–3 each):

| Area | Impact | Likelihood (recent change?) | Score | Depth |
|---|:---:|:---:|:---:|---|
| Payment capture | 3 | 3 (provider swapped) | **9** | Full suite + exploratory + data checks |
| Product search | 3 | 1 (untouched) | 3 | Smoke only |
| Footer links | 1 | 1 | 1 | Skip this round |

Present this table when someone asks "can we ship Friday?" — it turns a feeling into a decision.

## 7. Shift-left in practice (what it means for a manual QA)

- Review designs/mockups for edge cases *before* code exists ("what does the empty state look like?")
- Write test scenarios from acceptance criteria the day the story is refined
- Pair with the developer for 15 minutes *before* they merge — cheapest bugs you'll ever find
- Sit in on API design and flag untestable contracts

## ✅ Exercise

Your team must ship in 2 days. 40 test cases remain: 10 payment, 10 profile-settings, 10 admin reports, 10 email templates. The payment provider SDK was upgraded this sprint. Write your risk table and defend what you'll skip.

**Next →** [Stage 5: The QA Toolbox](06-tools.md)
