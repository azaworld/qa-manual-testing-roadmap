# Stage 9 — Soft Skills: What Actually Decides QA Careers

> **Goal:** master the human side of QA. Two testers with identical technical skills can be years apart in career growth — this chapter is the difference. I've led QA teams and hired testers; I promote for what's on this page.

## 1. Writing that people act on

Your bug reports, test summaries, and Slack messages ARE your reputation.

- **Lead with the point.** "Payment double-charges on slow networks — blocking release" first, details after. Busy people read the first line only.
- **Facts, not feelings.** ❌ "The app is very buggy" → ✅ "12 defects this cycle, 3 critical, all in the new coupon module"
- **Describe behavior, never blame.** ❌ "Your code crashes" → ✅ "The app crashes when…" The bug is in the software, not in a person.
- **Every claim carries evidence.** Screenshot, video, HAR, query result. Opinion is free; evidence is credibility.

## 2. Diplomacy — the bug messenger's art

You deliver bad news for a living. How you deliver it determines whether people thank you or avoid you.

| Situation | Weak move | Strong move |
|---|---|---|
| Dev says "not a bug" | Argue in comments | Re-check the requirement; if it's ambiguous, take it to the PM as a *requirements question*, not a fight |
| Dev says "works on my machine" | "Well it doesn't on mine" | Diff the environments together — build, data, flags. Make it a shared puzzle, not a standoff |
| PM wants to ship with a critical open | Silent resentment or loud protest | One page: impact in user terms, reproduction rate, options with costs. Recommend clearly, then respect the call — **it's their decision and your record** |
| You broke something with a wrong report | Hide it | Correct it fast and publicly. Owning mistakes buys more trust than being right ever did |

**The core stance:** you are not the quality police; you are the team's headlights. Same information, different relationship.

## 3. Asking questions — your sharpest tool

QA's superpower in refinement is the question nobody thought to ask:

- "What happens when the coupon expires *while* the user is in checkout?"
- "What does the empty state look like?"
- "Which of these two behaviors is correct? The spec says both."
- "Who is allowed to do this action — and what stops the others?"

Practice pattern: for any feature, ask **what if it's empty · what if it's huge · what if it happens twice · what if two people do it at once · what if it fails halfway.**

## 4. Saying no (and yes) with evidence

- Too much to test, too little time → don't heroically silently absorb it. Show the [risk table](05-agile-and-process.md#6-risk-based-testing--the-senior-skill): "In 2 days I can cover payment + auth deeply, or everything shallowly. Which do you want?"
- Asked to "just quickly sign off"? → "Here's what I ran and what I didn't. If those risks are acceptable, we can ship." You provide the truth; the business owns the risk.

## 5. Time & attention management

- **Batch context switches** — bug writing and test execution use different brains; alternate in blocks, not per-bug
- **Timebox exploration** — charters with a clock beat open-ended wandering
- **The daily anchor:** what's the *riskiest untested thing right now?* Start there, always
- Track your own flow: if you spend 40% of a day chasing environments, that's a process bug — raise it like one

## 6. Working across cultures & remote (real talk)

Much of QA hiring is global-remote. What wins:

- **Overcommunicate state.** End of day: what you ran, what you found, what's blocked. Nobody should wonder what QA did today
- **Async-first writing.** Assume your reader wakes up 6 hours after you wrote it — links, context, no "as discussed"
- **Simple English beats fancy English.** Short sentences. Bullet points. Screenshots. (Non-native speakers: clarity is the skill, not vocabulary — my career was built from Dhaka working with US/UK/EU teams)
- **Reliability is the currency.** Delivering exactly what you said, when you said, is rarer than talent

## 7. The meta-skills

- **Curiosity** — the "what does *this* button do under *those* conditions" instinct. Feed it daily
- **Skepticism without cynicism** — question everything, resent nothing
- **Learning in public** — write one LinkedIn post per month about a bug/lesson; a visible tester gets recruited, an invisible one applies
- **Mentoring early** — explaining EP to a newer tester locks in your own mastery and starts your leadership record now

## 8. The soft-skill interview questions (they're coming)

- "Tell me about a conflict with a developer" → have your [STAR story](08-interview-prep.md#round-3--behavioral-star-stories-to-prepare) ready; end with the *relationship intact*
- "A stakeholder pressures you to skip testing" → evidence + options + their call — never "I just refused"
- "How do you handle repetitive work?" → honesty + systems: checklists, rotation, and eventually automation of the boring parts

## ✅ Exercise

Rewrite this real (bad) bug comment to professional standard:
> "This is broken AGAIN!!! Dev team keeps breaking checkout, third time this month. Doesn't anyone test their code???"

Your version should: state the regression factually, link the three occurrences, propose a prevention (regression suite addition? merge checklist?), and blame nobody.

**Next →** [Stage 10: Sources & Further Learning](11-resources.md)
