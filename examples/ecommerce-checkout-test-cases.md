# Worked Example — E-commerce Checkout Test Cases

A realistic slice of a checkout suite showing named techniques in action. Feature under test: card checkout for a store with guest + member flows. Sandbox cards: `4242…4242` (success), `4000…0002` (decline), `4000…0069` (expired).

## Positive path

### TC-CHK-001 — Member completes card checkout successfully (P1)
**Technique:** happy path / E2E
**Preconditions:** logged-in member, 1 in-stock item ($25) in cart

| # | Action | Expected |
|---|---|---|
| 1 | Open cart, click Checkout | Checkout page loads; saved address pre-filled |
| 2 | Select saved card ending 4242, click Pay | Spinner shown; button disabled while processing |
| 3 | Wait for result | Order confirmation page with order number; total = $25 + tax/shipping per pricing rules |
| 4 | Check email inbox (test mail catcher) | Confirmation email within 2 min; order number matches |
| 5 | (Data check) `SELECT status FROM orders WHERE id = <order>` | `status = 'confirmed'`, exactly one payment row |

## Negative & boundary — where the bugs live

### TC-CHK-002 — Declined card shows recoverable error (P1)
**Technique:** EP (invalid payment partition)

| # | Action | Expected |
|---|---|---|
| 1 | Checkout with decline card `4000…0002` | Error: "Your card was declined…" — user stays on checkout with cart intact, can retry with another card |
| 2 | (Data check) orders table | **No** order row created; no charge recorded |

### TC-CHK-003 — Expired card is rejected client-side (P2)
**Technique:** EP + BVA on expiry date — test last month (reject), current month (accept — boundary!), next month (accept)

### TC-CHK-004 — Quantity boundaries (P2)
**Technique:** BVA. Max per order = 10.

| Quantity | Expected |
|---|---|
| 0 | Item removed or blocked with message |
| 1 | Accepted (lower boundary) |
| 10 | Accepted (upper boundary) |
| 11 | Blocked: "Maximum 10 per order" |
| -1 / `abc` (edit request in DevTools/Postman) | Server rejects with 400 — **client-side limits are not security** |

### TC-CHK-005 — Double-click Pay does not double-charge (P1)
**Technique:** error guessing (race condition). *This class of bug produced real production incidents I've caught in payment systems.*

| # | Action | Expected |
|---|---|---|
| 1 | DevTools → Network → throttle "Slow 3G" | |
| 2 | Double-click Pay rapidly | Button disables on first click; exactly ONE request to /payment in Network tab |
| 3 | Data check | Exactly one order, one payment row |

### TC-CHK-006 — Session expires mid-checkout (P2)
**Technique:** state transition. Fill checkout → wait past session timeout (or clear session cookie) → click Pay. Expected: redirect to login, cart preserved after re-login, **no charge**.

### TC-CHK-007 — Price changes between cart and pay (P2)
**Technique:** state/race. Admin lowers price while item sits in checkout. Expected per requirement — *this is a "go ask the PM" case: does the customer get old or new price? Get it in writing.*

### TC-CHK-008 — Coupon + free-shipping stacking (P2)
**Technique:** decision table — see [Stage 1](../02-test-design-techniques.md#3-decision-table-testing) for the full table; execute one case per rule R1–R6.

### TC-CHK-009 — Checkout on mobile with interruption (P2)
**Technique:** mobile interruption. Start payment on real device → receive a call at the spinner → return to app. Expected: payment resolves exactly once; UI reflects the true final state.

## Coverage summary

| Dimension | Cases |
|---|---|
| Happy paths | 001 |
| Payment failures | 002, 003 |
| Boundaries | 003, 004 |
| Race/timing | 005, 006, 007 |
| Business rules | 008 |
| Mobile | 009 |

9 cases, every one earning its place. That's test *design* — not 200 copy-pasted permutations.
