# Worked Example — A Bug Report Developers Love

*(Names and URLs genericized from a real class of bug found in production e-commerce work.)*

| Field | Value |
|---|---|
| **Title** | [Checkout] Customer charged twice when "Pay" is double-clicked on a slow connection |
| **Severity** | **Critical** — financial impact, customer-facing |
| **Priority** | Highest (proposed) |
| **Reproduction rate** | 4/5 on Slow-3G throttle; 0/5 on fast connection |
| **Environment** | staging build `2026.08.11-r3` (commit `a1b2c3d`), Chrome 128 / macOS 14, member account `qa-member-04`, no feature flags |
| **Found via** | Exploratory charter "attack checkout under bad network" |

## Steps to reproduce
1. Log in as `qa-member-04`; add any in-stock item to cart
2. Proceed to checkout with saved card ending 4242
3. DevTools → Network → throttling = **Slow 3G**
4. **Double-click** the Pay button quickly (< 300 ms apart)

## Expected result
Pay button disables on first click; one request to `POST /api/payment`; customer charged once; one order created.

## Actual result
Two `POST /api/payment` requests fire (see HAR); both return `201`. Two identical orders appear in order history; payment sandbox shows **two charges** of $27.14.

## Evidence
- 🎥 `double-charge-repro.mp4` (22s)
- 📎 `checkout-double-post.har` — both requests visible at 00:04.1 and 00:04.3
- 🖼️ `two-orders.png` — duplicate orders #88121 / #88122 circled
- Console: no JS errors (button never disables — root cause hint: no debounce/disable on submit handler)

## Notes for triage
- Workaround: none a customer would know
- Likely affects mobile users disproportionately (slow networks)
- Data check: `SELECT id FROM orders WHERE user_id=204 AND created_at > now()-interval '5 min';` → 2 rows
- Suggested guard (for discussion, dev's call): disable button on submit + idempotency key on /payment

---

### Why this report works
Symptom + trigger in the title → searchable. Repro rate with conditions → nobody wastes time on "can't reproduce." Evidence covers UI, network, and data layers → the fix conversation starts at root cause, not at "is this real?"
