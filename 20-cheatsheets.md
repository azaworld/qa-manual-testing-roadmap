# 📌 QA Cheatsheets

> **Goal:** fast, dense reference cards you can glance at (or put on screen while recording). No fluff — the things you look up mid-task. Inspired by [educative.io/cheatsheets](https://www.educative.io/cheatsheets), tuned for QA.

---

## 🌐 HTTP status codes

| Code | Meaning | QA note |
|---|---|---|
| **200** OK / **201** Created / **204** No Content | Success family | 201 for POST-create; 204 for delete/no-body |
| **301/302** Moved / Found | Redirects | Check the target and that it's HTTPS |
| **400** Bad Request | Client sent something invalid | Expected for missing/invalid fields |
| **401** Unauthorized | Not authenticated | Missing/expired/bad token |
| **403** Forbidden | Authenticated, not allowed | The IDOR/authz test target |
| **404** Not Found | No such resource | Someone else's id should be 403/404 — **not 200** |
| **409** Conflict | State clash | Double-submit, version conflict |
| **422** Unprocessable | Validation failed | Well-formed but semantically wrong |
| **429** Too Many Requests | Rate limited | Test login/OTP brute-force protection |
| **500/502/503** Server errors | Server broke | 500 where 400 belongs = unvalidated input reached the server |

🔎 *Demo live:* [httpbingo.org/status/404](https://httpbingo.org/status/404) returns any code on demand · [http.cat](https://http.cat/) for a memorable visual.

---

## 🧪 Test design techniques

| Technique | Use when | Example |
|---|---|---|
| **Equivalence Partitioning** | Grouped inputs | age 18–60 → one valid + one each invalid side |
| **Boundary Value Analysis** | Ranges/limits | test 17,18,19 and 59,60,61 |
| **Decision Table** | Combined rules | free shipping if (≥$50 AND member) OR coupon |
| **State Transition** | State machines | account lockout after 3 fails |
| **Pairwise** | Config explosion | 3×3×2 combos → ~9 pairs |
| **Error Guessing** | Experience | emoji, `<script>`, double-click, 0-byte file |

---

## 🐞 Severity vs Priority

| | High priority | Low priority |
|---|---|---|
| **High severity** | Payment charges twice | Crash in a yearly-use legacy report |
| **Low severity** | CEO's name misspelled on homepage | Tooltip typo in settings |

*Severity = impact (QA owns). Priority = fix order (product owns, you advise).*

---

## 🎭 Playwright quick reference

```bash
npm init playwright@latest         # scaffold
npx playwright test                # run all
npx playwright test --headed       # watch it run
npx playwright test --ui           # interactive UI mode
npx playwright codegen <url>       # record a test
npx playwright show-trace trace.zip# debug a failure
```

```typescript
await page.goto('/login');
await page.getByLabel('Email').fill('me@x.com');
await page.getByRole('button', { name: 'Sign in' }).click();
await expect(page.getByText(/welcome/i)).toBeVisible();
await expect(page).toHaveURL(/dashboard/);
```

*Locator priority:* `getByRole` > `getByLabel/Text` > `getByTestId` > CSS > (avoid) positional XPath.
🔎 *Docs live:* [playwright.dev](https://playwright.dev/)

---

## 🔌 Postman assertions (Tests tab)

```javascript
pm.test("status 200", () => pm.response.to.have.status(200));
pm.test("has id", () => pm.expect(pm.response.json().id).to.be.a("number"));
pm.test("fast", () => pm.expect(pm.response.responseTime).to.be.below(800));
pm.test("schema", () => pm.response.to.have.jsonSchema(schema));
```

```bash
newman run collection.json -e staging.json   # run in CI
```
🔎 *Practice live:* [reqres.in](https://reqres.in/) · [restful-booker](https://restful-booker.herokuapp.com/) · [Postman Echo](https://postman-echo.com/)

---

## 🗄️ SQL for QA (the 5 that cover 90%)

```sql
SELECT * FROM orders WHERE id = 8812;                       -- did it persist?
SELECT COUNT(*) FROM orders WHERE user_id=42 AND status='shipped';
SELECT email, COUNT(*) FROM users GROUP BY email HAVING COUNT(*)>1;  -- dupes
SELECT o.id FROM orders o LEFT JOIN invoices i ON i.order_id=o.id
  WHERE o.status='paid' AND i.id IS NULL;                   -- cross-table gaps
SELECT * FROM audit_log WHERE entity_id=8812 ORDER BY created_at DESC LIMIT 20;
```
*Read-only on staging. Never write.* 🔎 *Practice live:* [SQLBolt](https://sqlbolt.com/) · [DB Fiddle](https://www.db-fiddle.com/)

---

## ⚡ k6 performance

```javascript
export const options = {
  stages: [ {duration:'2m',target:200}, {duration:'5m',target:200}, {duration:'2m',target:0} ],
  thresholds: { http_req_duration:['p(95)<500'], http_req_failed:['rate<0.01'] },
};
```
```bash
k6 run script.js
```
| Test | Shape |
|---|---|
| Load | ramp → hold → down |
| Stress | ramp past breaking point |
| Spike | sudden jump → drop |
| Soak | moderate, held for hours |
🔎 *Practice live:* [test.k6.io](https://test.k6.io/) · *docs:* [grafana.com/docs/k6](https://grafana.com/docs/k6/latest/)

---

## 🔐 OWASP Top 10 (QA lens)

| Risk | Quick manual test |
|---|---|
| Broken Access Control | Change resource id / role in the request (IDOR) |
| Injection | `' OR '1'='1' --`, `<script>alert(1)</script>` |
| Crypto Failures | HTTPS everywhere? tokens/PII in URLs/logs? |
| Security Misconfig | Stack traces shown? default creds? |
| Auth Failures | Lockout? session invalidated on logout? |
🔎 *Practice live:* [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) · *learn:* [PortSwigger Academy](https://portswigger.net/web-security)

---

## 🧠 AI × QA quick start

```bash
claude mcp add playwright -- npx @playwright/mcp@latest   # AI drives a real browser
```
- **Prompt for test ideas:** *"Act as a senior QA — what conditions am I missing? Focus on boundaries, states, concurrency."*
- **Eval tools:** [promptfoo](https://promptfoo.dev/) · [DeepEval](https://github.com/confident-ai/deepeval)
- **Rule:** AI drafts, you decide. Always verify.

---

## 🛠️ Handy dev/QA utilities (bookmark these)

| Need | Site |
|---|---|
| Fake REST API | [jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com/) |
| Inspect your request | [httpbingo.org](https://httpbingo.org/) |
| Test regex | [regex101.com](https://regex101.com/) |
| Decode a JWT | [jwt.io](https://jwt.io/) |
| Validate/format JSON | [jsonlint.com](https://jsonlint.com/) |
| Explain a cron expression | [crontab.guru](https://crontab.guru/) |
| Catch test emails | [Mailinator](https://www.mailinator.com/) · [Mailtrap](https://mailtrap.io/) |
| Cross-browser/device cloud | [BrowserStack](https://www.browserstack.com/) |

← Back to [the roadmap](README.md) · **Next →** [Teaching Kit & Demo Sites](21-teaching-kit.md)
