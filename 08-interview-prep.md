# Stage 7 — Interview Preparation (the complete playbook)

> **Goal:** walk into any QA interview knowing exactly what each round tests, how to prepare for it, and how to answer — from the recruiter call to the salary negotiation. This chapter is the **strategy and process**; the actual questions with model answers live in the **[Interview Bank (Top 100+)](19-interview-bank.md)**. Use them together: read the process here, drill the questions there.

Interviews aren't a memory test — they're a **simulation of working with you**. Every round is really asking one thing: *"Is this someone I trust to own quality on my team?"* Everything below serves that.

---

## 1. The QA interview process, end to end

Most QA hiring runs through 3–5 rounds. Knowing the shape removes the fear:

| # | Round | Who runs it | What they're really testing | How you win it |
|---|---|---|---|---|
| 1 | **Recruiter / HR screen** (20–30 min) | Recruiter | Basics, communication, salary fit, motivation | Clear 90-second intro, know the company, have a salary range ready |
| 2 | **Technical / concept round** (45–60 min) | QA lead / senior | Fundamentals: test design, severity, SDLC, API, automation | Structured answers with examples — see [Interview Bank](19-interview-bank.md) |
| 3 | **Practical / hands-on task** | QA team | *Can you actually do the job?* | Narrate your thinking; quality over quantity (script below) |
| 4 | **Behavioral round** (45 min) | Hiring manager | Collaboration, ownership, conflict, judgment | STAR stories, relationships intact |
| 5 | **Panel / values / bar-raiser** (optional) | Cross-functional | Culture, cross-team communication | Consistency + genuine questions for them |

> 💡 **Ask the recruiter for the format up front.** "Could you tell me the interview stages and what each involves?" is a normal, professional question — and it lets you prepare precisely.

---

## 2. Before the interview: what actually gets you in the room

You're assessed before you speak. Invest here first — details in [Career Journey](07-career-journey.md):

- **Résumé that proves outcomes.** Every bullet = *action + object + result*: "Designed 120 test cases (EP/BVA) for checkout; found 14 pre-release defects including a double-charge bug" beats "responsible for testing."
- **A public portfolio.** A repo with a test plan, 25–40 test cases, polished bug reports, a Postman collection, and ideally a green Playwright CI run. This is the single biggest differentiator — build it via [The Playground](17-playground.md).
- **A findable presence.** LinkedIn up to date; GitHub pinned repos; a few posts about bugs you've found. Recruiters search for you.
- **Company research.** Their product, who their users are, what "quality" means for them (a bank ≠ a game), recent news, and the exact job description — mirror its language.

---

## 3. Round 1 — The recruiter screen

**What it is:** a fit-and-filter call. Friendly, but it decides whether you advance.

**Prepare three things:**
1. **Your 90-second intro** — who you are, your QA focus, one signature achievement, what you're looking for. Practice it out loud.
2. **"Why us?"** — one specific, genuine reason tied to their product or mission.
3. **A salary range** — research it ([Levels.fyi](https://www.levels.fyi/), [Glassdoor](https://www.glassdoor.com/), local market) and give a *range*, not a number, if pushed early.

**Common openers:** "Tell me about yourself," "Why are you leaving?", "What are you looking for?", "What's your salary expectation?" Keep answers short and positive — never bad-mouth a current/past employer.

---

## 4. Round 2 — The technical / concept round

**What it is:** rapid and deep questions on fundamentals. This is where the [Interview Bank](19-interview-bank.md) does the heavy lifting — drill the **Top 20** until they're automatic, then the category banks matching the role (add API/automation/AI for SDET roles).

**The technique that impresses:** answer with **structure, then an example.**
> ❌ *"I'd test the login by trying different passwords."*
> ✅ *"I'd organize by dimension — functional, boundary, security, usability, compatibility, state — then prioritize by risk. For example, on the security dimension I'd test lockout after N failed attempts and that the password field is masked and sent over HTTPS."*

**If you don't know something:** say so, then reason out loud. "I haven't used that tool, but based on how X works I'd expect… and I'd verify by…" Testers are hired for *how they think*, not for trivia recall.

---

## 5. Round 3 — The practical / hands-on task

Almost every QA hire includes one. This is where offers are won or lost — **narrate your thinking the entire time.** The method *is* the answer.

| Task you'll get | What they grade | Your move |
|---|---|---|
| "Test this page/app for 30 min" | Structure, bug quality, prioritization | Use the exploratory script below |
| "Write test cases for X" | Technique names, negatives, precise expected results | Name EP/BVA/decision tables as you go |
| "Critique this bug report" | Do you spot missing repro/env/evidence? | Check it against the [template](templates/bug-report-template.md) |
| "Write a bug report for this defect" | Clarity a dev can act on | Symptom+condition title, repro, expected vs actual, evidence |
| "Take-home assignment" | Real-world craft + communication | Treat it like production; add a README explaining choices |

### The 30-minute exploratory script (memorize this)
1. **Recon (5 min)** — map the feature; state your charter out loud: *"I'll explore checkout with invalid payments and coupon stacking to find pricing and state bugs."*
2. **Attack (20 min)** — one area at a time: boundaries, negative inputs, error-guessing (double-click, back button, refresh mid-flow), interruptions. Log each finding as you go.
3. **Report (5 min)** — bugs first, ordered by severity; then coverage notes; then open questions. *"Here's what I found, what I'd test next with more time, and what I'd ask the PM."*

Practice this live on the [Teaching Kit demo sites](21-teaching-kit.md) — e.g. SauceDemo's `problem_user`.

---

## 6. Round 4 — The behavioral round

**What it is:** stories about how you actually work. They're checking ownership, collaboration, and judgment under pressure.

### The STAR framework
Structure every answer as:
- **S**ituation — one sentence of context
- **T**ask — what you needed to achieve
- **A**ction — *what you personally did* (the meat — spend most time here)
- **R**esult — the outcome, with a number if possible, and what you learned

**Worked example — "Tell me about a conflict with a developer":**
> **S:** A developer marked my critical bug "cannot reproduce" the day before release.
> **T:** I needed it taken seriously without turning it into a standoff.
> **A:** I re-ran it and captured a screen recording plus the HAR file, then noticed my build was one commit ahead of theirs. I shared the evidence in the ticket, framed it as "here's the exact environment," and we paired for ten minutes.
> **R:** We found it was a config difference; the fix shipped on time. We started pinning build versions in every bug report after that — the process improved, and our working relationship got stronger.

### Prepare 5 stories (reuse them across many questions)
1. A bug you're proud of finding (required thinking, not luck)
2. A disagreement over severity/priority — resolved with the relationship intact
3. A release you recommended against, or a bug that escaped and what you changed
4. Handling too much to test in too little time
5. Something you improved or automated

Full question list: [Interview Bank — Behavioral](19-interview-bank.md).

---

## 7. What changes by level (know your target)

| | **Junior QA** | **Mid-level QA** | **Senior QA / SDET** |
|---|---|---|---|
| They test for | Solid fundamentals, coachability, clean bug reports | Independent ownership of a feature; API/automation | Judgment, strategy, influence, mentoring |
| Practical task | Test cases + exploratory | + API testing, a small automation script | + framework design, risk-based strategy, "how would you test our system?" |
| Behavioral | Attitude, communication | Collaboration, prioritization | Leadership, stakeholder management, tough calls |

Pitch yourself at the level you're interviewing for — a senior answer to a junior role is fine; a junior answer to a senior role is a fail.

---

## 8. Questions YOU should ask them

Interviews are two-way. Asking sharp questions signals seniority *and* protects you from a bad team. Have 3–4 ready:

- "What's your defect **escape rate**, and do you track it?" *(metric literacy)*
- "Where does QA sit in the sprint — from refinement, or after dev-complete?" *(shift-left maturity)*
- "What's the ratio of manual to automated regression, and who owns automation?"
- "What does your release gate / definition of done look like?"
- "What does success in this role look like at 3 and 6 months?"
- *(to a manager)* "How does the team handle a bug that escaped to production?"

Their answers tell you whether the QA culture is healthy — you're interviewing them too.

---

## 9. Remote & online-interview logistics

Most QA hiring is remote. Small things read as professionalism:

- **Test your setup** an hour before: camera, mic, stable internet, the screen-share/coding tool they'll use.
- **Environment:** quiet, tidy background, good lighting, phone silenced.
- **Have ready:** your résumé, the job description, a notepad, water, and (for practical rounds) your IDE/Postman/browser pre-opened.
- **Screen-share cleanly:** close personal tabs and notifications before you share.
- **Eye contact = look at the camera,** not the face on screen, for key moments.

---

## 10. Salary & offer conversations (professional basics)

> ⚠️ Career-general guidance, not financial advice — decisions are yours.

- **Research first:** [Levels.fyi](https://www.levels.fyi/), [Glassdoor](https://www.glassdoor.com/), local market rates for the level and location.
- **Deflect early, anchor with a range:** if asked before an offer, "I'm looking in the range of X–Y based on the role and market — I'm flexible depending on the full package."
- **Evaluate the whole offer:** base, bonus, equity, benefits, remote flexibility, growth, the team.
- **Negotiate calmly and once:** "I'm excited about this. Based on my experience and the market, is there flexibility on the base?" Then decide. Be gracious either way.

---

## 11. Common mistakes to avoid

- ❌ "I test **everything**." (Nobody can — show how you *prioritize by risk*.)
- ❌ Blaming developers or past employers, ever.
- ❌ Vague expected results — "it should work fine." Be specific and checkable.
- ❌ Answering a *thinking* question with "I'd just automate it."
- ❌ Memorized answers with no example — always ground it in something you did.
- ❌ No questions for them — reads as low interest.
- ❌ On practical tasks: clicking silently. **Narrate.**

---

## 12. Your preparation timeline

**2 weeks out**
- [ ] Polish résumé + portfolio; align with the job description
- [ ] Drill the [Interview Bank](19-interview-bank.md) Top 20 + role-specific banks
- [ ] Write your 5 STAR stories

**1 week out**
- [ ] Run the [30-min mock interview](19-interview-bank.md) out loud (record yourself)
- [ ] Practice the exploratory script on a [demo site](21-teaching-kit.md)
- [ ] Research the company; prepare your questions for them

**Day before**
- [ ] Confirm time/timezone/tools; test camera + mic
- [ ] Re-read the job description and your own résumé
- [ ] Sleep

**Day of**
- [ ] Setup tested, tabs closed, résumé + notepad ready
- [ ] Arrive 5 minutes early, calm, water nearby

---

## 13. Resources (verified)

- **[Interview Bank (this roadmap)](19-interview-bank.md)** — Top 100+ Q&A with model answers + mock protocol
- [Ministry of Testing – The Club](https://club.ministryoftesting.com/) — community, mock partners, interview threads
- [Guru99 — QA interview questions](https://www.guru99.com/software-testing-interview-questions.html)
- [Glassdoor](https://www.glassdoor.com/) — search real questions for your target company
- [Levels.fyi](https://www.levels.fyi/) — compensation benchmarks
- [Pramp](https://www.pramp.com/) · [interviewing.io](https://interviewing.io/) — free peer mock interviews
- 🎓 [AZADEMY](https://azademy.vercel.app/) — guided interview prep & mock drills with feedback

---

> **Bottom line:** preparation converts anxiety into confidence. Know the rounds, drill the questions, rehearse out loud, and bring a portfolio that proves you can do the job. Then walk in and have a good conversation about quality.

**Next →** [Stage 8: Path to Automation](09-path-to-automation.md) · or drill the [Interview Bank](19-interview-bank.md)
