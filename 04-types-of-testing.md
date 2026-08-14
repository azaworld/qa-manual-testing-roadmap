# Stage 3 — Types of Testing (and when to use each)

> **Goal:** know the full testing landscape so you always pick the right kind of testing for the risk in front of you.

## The map

```
                        ┌── Functional ── does it do the right thing?
        What you test ──┤
                        └── Non-functional ── does it do it well? (speed, security, usability)

                        ┌── Smoke → Sanity → Regression → UAT   (by purpose)
        When you test ──┤
                        └── Unit → Integration → System → Acceptance   (by level)
```

## 1. Functional testing — by purpose

| Type | What it is | When you run it | Manual example |
|---|---|---|---|
| **Smoke** | "Is the build alive?" — 10–30 min of critical paths | Every new build, before anything else | App opens, login works, one product adds to cart, checkout page loads |
| **Sanity** | Quick check that a *specific fix/feature* works | After a bug fix or small change | Bug said coupon fails — apply one coupon, confirm total |
| **Regression** | Did the change break anything *else*? | Before every release; after risky merges | Full checkout suite after a payment-provider update |
| **Re-testing** | Verify a specific defect is fixed (run the exact failing steps) | When a bug moves to "fixed" | Re-run BUG-2231's repro steps on the new build |
| **UAT** | Business/users confirm it solves the real problem | End of cycle, before ship | Store manager processes a real return end-to-end |
| **End-to-End** | A complete user journey across systems | Major flows, every release | Order → payment → warehouse EDI → shipping confirmation email *(I ran these across 5 marketplace portals)* |

## 2. Non-functional testing — the "how well"

| Type | What you check | Manual techniques |
|---|---|---|
| **Usability** | Can a human actually use it? | Watch a non-team-member complete a task; note every hesitation |
| **Accessibility** | Works for users with disabilities (WCAG) | Keyboard-only navigation, screen reader pass, color-contrast check, zoom to 200% |
| **Compatibility** | Browsers, devices, OS versions | Matrix testing — prioritize by your real traffic analytics, use BrowserStack for the long tail |
| **Localization** | Languages, currencies, formats | German strings 2× longer than English (layout breaks), RTL for Arabic, date formats |
| **Performance (manual level)** | Perceived speed, obvious slowness | DevTools network throttling, watch spinners, note anything > 3s |
| **Security (manual level)** | Obvious holes | Try other users' URLs (IDOR), inspect what the API returns vs what's shown, test role permissions, `<script>` in inputs |
| **Recovery/negative** | Behavior under failure | Kill network mid-payment, force-close app during sync, submit while session expired |

Performance and security have deep specialist ends — as a manual QA you find the *first layer* and escalate. Go deeper in the specialist tracks: [Performance Testing](16-performance-testing.md) (k6/JMeter, load/stress/spike/soak) and [Security Testing](14-security-testing.md) (OWASP Top 10, ZAP/Burp).

## 3. API testing — manual, with Postman

You don't need code to test APIs, and it makes you 2× more valuable:

1. Get the endpoint list (Swagger/OpenAPI docs)
2. In Postman: send a valid request → check **status code** (200/201), **response body** (fields, types, values), **response time**
3. Now attack it: missing required fields (expect 400), wrong auth token (401), someone else's resource ID (403/404 — **not** 200!), malformed JSON, huge payloads
4. Cross-check the UI against the API: if the API returns 20 orders and the UI shows 18 — that's a bug nobody else would have found

## 4. Mobile testing — what's different

- **Interruptions:** incoming call mid-checkout, notification swipe, app backgrounded during payment
- **Network reality:** airplane mode mid-request, WiFi→cellular handoff, 3G throttle
- **Device matrix:** small screens, notches, Android back button, iOS gestures
- **Permissions:** deny camera/location, then use the feature that needs it
- **Real devices beat emulators** for touch, camera, and performance feel — device clouds (BrowserStack, AWS Device Farm) give you the fleet

## 5. Data & integration testing (the differentiator)

Where senior manual QA lives — behind the UI:

- **SQL checks:** the UI says the order is "shipped" — does the database row agree? `SELECT status FROM orders WHERE id = 8812;`
- **EDI/document flows:** in supply-chain work, an order isn't done until the X12 856 (ship notice) and 810 (invoice) match the 850 (order). I've validated these flows for Amazon/Walmart/Target/Chewy integrations — the bugs hide in the documents, not the UI.
- **Email/SMS/webhooks:** trigger them, actually receive them, check every merge field

## ✅ Exercise

For a signup flow, name which testing type catches each of these:
1. Signup button broken in yesterday's build *(smoke)*
2. Works in Chrome, dead in Safari *(compatibility)*
3. Password accepted but user can't log in after — DB row missing *(E2E + data check)*
4. Welcome email says "Hello {firstName}" *(integration/email)*
5. Screen reader reads the T&C checkbox as "checkbox" with no label *(accessibility)*

**Next →** [Stage 4: QA in Agile Teams](05-agile-and-process.md)
