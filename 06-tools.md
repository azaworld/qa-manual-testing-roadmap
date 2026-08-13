# Stage 5 — The QA Toolbox

> **Goal:** master the tools you'll touch every single day. None of these require code.

## 1. Jira (or any tracker) — where your work lives

- Write stories/bugs with the [bug template](templates/bug-report-template.md) baked into a Jira template
- Learn **JQL** basics — 10× faster than clicking filters:
  - `project = SHOP AND status = "Ready for Retest" AND assignee = currentUser()`
  - `type = Bug AND priority in (Highest, High) AND created >= -7d`
- Link everything: bug → story → test case. Future-you will thank present-you.

## 2. Test management — TestRail / QASE / Xray

Where suites, runs, and results live. The workflow: **suite → test run (per release/build) → execute & record → report**. Keep suites pruned — a 3,000-case suite nobody runs is worse than a 300-case suite that's green weekly (pesticide paradox!). I use QASE on live client programs; TestRail is the most common in job listings.

## 3. Browser DevTools — your microscope (F12)

| Tab | What you catch |
|---|---|
| **Console** | JS errors after any action — a red stack trace turns "weird behavior" into a great bug report |
| **Network** | The request behind the button: status code, payload, response, timing. Filter XHR, right-click → **Copy as cURL** → paste into the bug |
| **Network → throttling** | "Slow 3G" reveals race conditions, double-submits, missing spinners |
| **Application** | Cookies, localStorage, session — clear them to test first-visit behavior |
| **Device toolbar** | Quick responsive checks before reaching for real devices |
| **Lighthouse** | One-click performance/accessibility/SEO audit with receipts |

**The HAR file trick:** Network tab → export HAR → attach to the bug. The developer sees *exactly* what happened. Instant credibility.

## 4. Postman — API testing without code

- Import the team's OpenAPI/Swagger spec — get every endpoint ready to fire
- **Environments** for dev/staging/prod base URLs and tokens
- **Collections** = reusable API test suites; the Collection Runner executes them in order
- Status code + body + response time on every call; save example responses as documentation

## 5. SQL — the manual tester's superpower

The five queries that cover 90% of QA needs:

```sql
-- Did the UI action actually persist?
SELECT * FROM orders WHERE id = 8812;

-- How many, really?  (UI pagination lies sometimes)
SELECT COUNT(*) FROM orders WHERE user_id = 42 AND status = 'shipped';

-- Duplicates that shouldn't exist (double-submit bugs)
SELECT email, COUNT(*) FROM users GROUP BY email HAVING COUNT(*) > 1;

-- Cross-table truth: paid orders missing invoices
SELECT o.id FROM orders o LEFT JOIN invoices i ON i.order_id = o.id
WHERE o.status = 'paid' AND i.id IS NULL;

-- Recent state changes while you were testing
SELECT * FROM audit_log WHERE entity_id = 8812 ORDER BY created_at DESC LIMIT 20;
```

Read-only access to staging DB. Never write. Ever.

## 6. Evidence tools — screenshots & screen recording

- Annotated screenshot > paragraph of description. Circle the problem.
- 15–30s video for anything with timing/steps (macOS: Cmd+Shift+5; Windows: Xbox Game Bar; or Loom)
- Name files meaningfully: `BUG-2231-double-charge-repro.mp4`

## 7. Proxy tools — Charles / mitmproxy (intermediate)

See and modify traffic between app and server — essential for **mobile** testing (point the phone's WiFi proxy at Charles):
- Throttle or kill specific endpoints (how does the app handle a 500 from /payment?)
- Rewrite a response to force rare states (empty list, 10,000 items, malformed JSON)

## 8. The supporting cast

- **BrowserStack / AWS Device Farm** — real device & browser matrix in the cloud
- **Mailtrap / Mailinator** — catch outgoing emails in test environments
- **JSONLint / jq** — validate and slice API payloads
- **WAVE / axe DevTools** — accessibility scans
- **Clipboard managers & text expanders** — repro steps and test data at your fingertips

## ✅ Exercise

1. Open any e-commerce site with DevTools Network tab on. Add to cart. Find the API call, its payload, and its response
2. Export the HAR
3. Throttle to Slow 3G and double-click "add to cart" — watch for duplicate requests. Congratulations, you're now testing like a professional.

**Next →** [Stage 6: Career Journey](07-career-journey.md)
