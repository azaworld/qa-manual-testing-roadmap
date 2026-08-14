# 🎬 Teaching Kit — Live Sites to Teach From (no slides)

> **For the instructor (that's you, or anyone teaching from this roadmap):** every section below maps to a **real, live website you can screen-share** and a short **"demo this"** script. Open the tab, share your screen, and *show* it — no slides to build. All sites are free, public, and safe to demonstrate on.

> ⚠️ **Ethics:** the security/performance targets below are explicitly built for practice. Never demo attacks or load tests against sites you don't own or aren't authorized to use.

**Legend:** 🖥️ = open & screen-share · 🎙️ = what to say/show on camera.

---

## Section: Foundations & the tester's mindset → [Stage 0](01-foundations.md)
- 🖥️ [SauceDemo](https://www.saucedemo.com/) — log in as **`problem_user` / `secret_sauce`** (images/layout are deliberately broken)
- 🎙️ *"A developer asks 'how do I make this work?' A tester asks 'how could this break?'"* Log in as `problem_user`, point at the broken product images live — that's the mindset in 10 seconds. Then contrast with `standard_user`.

## Section: Test design (EP / BVA / decision tables) → [Stage 1](02-test-design-techniques.md)
- 🖥️ [DemoQA Practice Form](https://demoqa.com/automation-practice-form) · [the-internet / inputs](https://the-internet.herokuapp.com/inputs)
- 🎙️ On the number input, demo **BVA** live: type the boundary values and show accept/reject. On the form, demo **EP** — one valid + one each invalid partition. Show how 5 smart inputs beat 50 random ones.

## Section: Bug reports & test cases → [Stage 2](03-test-artifacts.md)
- 🖥️ SauceDemo `problem_user` + your [Bug Report template](templates/bug-report-template.md) side-by-side · browser **DevTools (F12)**
- 🎙️ Find the broken image bug live, then fill the template on camera: title = symptom+condition, repro steps, expected vs actual, and press F12 → Network → **Copy as cURL** / export HAR to attach as evidence. Show a *good* vs *bad* bug title.

## Section: Testing types → [Stage 3](04-types-of-testing.md)
- 🖥️ **Responsive/compatibility:** DevTools device toolbar on any site · [BrowserStack](https://www.browserstack.com/) (free trial)
- 🖥️ **Accessibility:** [WAVE](https://wave.webaim.org/) — paste any URL for a live a11y audit · axe DevTools
- 🖥️ **API layer:** [ReqRes](https://reqres.in/)
- 🎙️ Run WAVE on a real homepage and read the contrast/label errors aloud. Toggle DevTools device mode to show a layout break. One tab per testing type.

## Section: Agile, defect lifecycle & tools → [Stage 4](05-agile-and-process.md) · [Stage 5](06-tools.md)
- 🖥️ [GitHub Issues](https://github.com/azaworld/qa-roadmap/issues) (free, live tracker) · browser **DevTools** · [Jira free trial](https://www.atlassian.com/software/jira/free)
- 🎙️ Create a real issue live to show the defect lifecycle (New → Triaged → …). In DevTools, open **Console** (show a JS error), **Network** (throttle to Slow 3G, show a slow call), and **Application** (clear cookies to test first-visit).

## Section: API testing → [Stage 12](13-api-testing-deep-dive.md)
- 🖥️ [Swagger Petstore](https://petstore.swagger.io/) — *the* live API teaching tool (try requests in-browser) · [restful-booker](https://restful-booker.herokuapp.com/) · [httpbin](https://httpbin.org/) · [JSONPlaceholder](https://jsonplaceholder.typicode.com/) · **Postman**
- 🖥️ **GraphQL:** [Countries GraphQL playground](https://countries.trevorblades.com/)
- 🎙️ On Petstore, fire a GET and read status/body/headers aloud; then send a bad request and show the 400. On httpbin hit `/status/500` and `/delay/3`. In the GraphQL playground, over-fetch fields to show field-level testing.

## Section: Automation (Playwright) → [Stage 8](09-path-to-automation.md) · [Stage 14](15-automation-deep-dive.md)
- 🖥️ [playwright.dev](https://playwright.dev/) (docs) · target = [SauceDemo](https://www.saucedemo.com/) · **`npx playwright codegen saucedemo.com`** (record live) · [Playwright Trace Viewer online](https://trace.playwright.dev/) · your [GitHub Actions](https://github.com/azaworld/qa-roadmap/actions)
- 🎙️ Run `codegen` on camera — click through login and watch code generate, then *rewrite* it with role-based locators + a page object. Drop a trace into trace.playwright.dev and step through the timeline. Show a green CI run.

## Section: Performance (k6) → [Stage 15](16-performance-testing.md)
- 🖥️ [test.k6.io](https://test.k6.io/) (safe target) · [k6 docs](https://grafana.com/docs/k6/latest/) · [play.grafana.org](https://play.grafana.org/) (live dashboards)
- 🎙️ Run a small `k6 run` in the terminal and read the p95 / throughput / error-rate output aloud. Open play.grafana.org to show what latency/throughput dashboards look like during a test.

## Section: Security (OWASP) → [Stage 13](14-security-testing.md)
- 🖥️ [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) (run locally, or the project's hosted demo) · [PortSwigger Web Security Academy](https://portswigger.net/web-security) (free live labs) · [OWASP ZAP](https://www.zaproxy.org/)
- 🎙️ On Juice Shop, demo an **IDOR** (change an id in the URL/request) and a reflected **XSS** in the search box. In a PortSwigger lab, walk one access-control lab end to end. Keep it strictly on these practice targets.

## Section: AI × QA + MCP → [Stage 11](12-ai-for-qa.md)
- 🖥️ [Claude Code](https://www.claude.com/product/claude-code) / [Cursor](https://cursor.com/) with [Playwright MCP](https://github.com/microsoft/playwright-mcp) · [promptfoo](https://promptfoo.dev/) · target = any demo site above
- 🎙️ Run `claude mcp add playwright …` live, then ask the agent *"open SauceDemo, add a backpack, check out, tell me what's broken, and write a Playwright test."* Show it driving a real browser, then **review the generated assertions** on camera — that's the QA job. Build one tiny promptfoo eval.

## Section: Interviews & mock → [Stage 7](08-interview-prep.md) · [Interview Bank](19-interview-bank.md)
- 🖥️ [Interview Bank](19-interview-bank.md) (your question set) · [Pramp](https://www.pramp.com/) · [interviewing.io](https://interviewing.io/)
- 🎙️ Screen-share the Interview Bank and answer 5 rapid-fire questions live, then do the 30-minute mock protocol on camera as a worked example.

---

## 🧰 Instructor's always-open tab set

Keep these pinned while recording any QA lesson:

| Tab | For |
|---|---|
| [SauceDemo](https://www.saucedemo.com/) | UI demos & bugs |
| [Swagger Petstore](https://petstore.swagger.io/) | API demos |
| [httpbin](https://httpbin.org/) | show any request/response/status |
| [regex101](https://regex101.com/) | regex & data validation |
| [jwt.io](https://jwt.io/) | decode tokens |
| [jsonlint](https://jsonlint.com/) | format/validate JSON |
| [crontab.guru](https://crontab.guru/) | explain schedules |
| DevTools (F12) | the QA microscope, on any site |

## 🎥 Recording tips
- One concept = one tab. Open it *before* you hit record.
- Do the thing live; narrate the *why*, not just the clicks.
- Show a failure, not just the happy path — that's what teaches testing.
- Point people to the matching roadmap chapter + [Cheatsheet](20-cheatsheets.md) in your description.

> 🎓 This whole roadmap is built to be recorded from. Publish the videos on **[AZADEMY](https://azademy.vercel.app/)** and link each lesson back here.

← Back to [the roadmap](README.md) · **See also:** [Cheatsheets](20-cheatsheets.md) · [Interview Bank](19-interview-bank.md)
