# Stage 7 — Interview Preparation

> **Goal:** walk into a QA interview with answers for the questions that actually get asked — and the practical tasks that follow them. I've sat on both sides of this table many times.

## Round 1 — Concept questions (with model answers)

**Q: Severity vs priority?**
> Severity is technical impact; priority is business urgency. High severity + low priority: a crash in a report two users open yearly. Low severity + high priority: the CEO's name misspelled on the homepage. QA sets severity; priority is decided with product.

**Q: You find a critical bug the night before release. What do you do?**
> Reproduce it and pin down the exact conditions and rate. Gather evidence (video, logs, HAR). Escalate immediately to the release owner with impact stated in user terms. Propose options: fix & retest the area, feature-flag it off, or ship with a documented workaround. **The decision is the business's; the evidence is mine.** What I never do: sit on it, or quietly "approve."

**Q: How do you test a login page?** (They're testing structure, not volume.)
> I'd organize by dimension: functional (valid/invalid combos via equivalence partitioning), boundaries (password length limits), security (SQL injection strings, XSS, rate limiting/lockout, password masking, HTTPS), usability (error message clarity, tab order), compatibility (browser matrix), and state (already-logged-in user visits /login, expired session, "remember me"). Then I'd prioritize by risk — auth is always high-impact.

**Q: What if the developer says "it works on my machine"?**
> That's data, not a rejection. I compare environments — build version, browser, account state, data. I attach a video + HAR so they see my exact reality. Most "works on my machine" bugs are environment or data differences, and finding *that* difference is the actual bug hunt.

**Q: A requirement is ambiguous. What do you do?**
> Ask before I test — in refinement if possible. I write down my assumption, get it confirmed by the PM in writing (ticket comment), and turn it into an acceptance criterion so the ambiguity dies permanently.

**Q: How do you decide what NOT to test?**
> Risk-based: impact × likelihood of change. Untouched, low-traffic areas get smoke coverage only. I document what was descoped and get sign-off — descoping silently is how trust dies.

## Round 2 — The practical task

Almost every manual QA hire includes one of these:

| Task | What they grade |
|---|---|
| "Test this page/app for 30 minutes" | Structure (do you use charters/dimensions or click randomly?), bug quality over quantity, prioritization of what you report first |
| "Write test cases for X" | Technique names (EP/BVA), negative cases, precise expected results |
| "Here's a bug report — critique it" | Do you spot missing repro steps, environment, evidence, vague expected-vs-actual? |
| "Write a bug report for this defect" | Use the [template](templates/bug-report-template.md) shape from memory |

**The 30-minute exploratory script:** 5 min recon (map the feature) → 20 min attack (one charter per area, boundaries + error guessing + interruptions) → 5 min report (bugs first by severity, then coverage notes, then open questions). Narrate your thinking out loud — the *method* is what they're buying.

## Round 3 — Behavioral (STAR stories to prepare)

Have one prepared story for each — from real work, coursework, or your portfolio project:

1. A bug you're proud of finding (make it one that required *thinking*, not luck)
2. A time you disagreed with a developer/PM about severity — and how it resolved
3. A release you recommended against — or a bug that escaped and what you changed after
4. How you handled having too much to test and too little time
5. Something you automated/streamlined (even a checklist counts)

Structure: **S**ituation (1 sentence) → **T**ask → **A**ction (the meat) → **R**esult (numbers if possible).

## Questions YOU should ask them

- "What's your defect escape rate — do you track it?" *(shows metric literacy)*
- "Where does QA sit in the sprint — refinement onward, or after dev-complete?" *(reveals shift-left maturity)*
- "What's the ratio of manual to automated regression, and who owns automation?"
- "What does your release gate look like?"

Their answers tell you if the QA culture is healthy — you're interviewing them too.

## Red flags in *your* answers to avoid

- ❌ "I test everything" (nobody does; say how you prioritize)
- ❌ Blaming developers, ever
- ❌ "I'd automate it" as an answer to a manual-thinking question
- ❌ Vague expected results ("it should work fine")

**Next →** [Stage 8: Path to Automation](09-path-to-automation.md)
