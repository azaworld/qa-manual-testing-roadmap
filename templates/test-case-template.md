# Test Case Template

| Field | Value |
|---|---|
| **ID** | TC-[AREA]-[###] e.g. TC-CHK-004 |
| **Title** | *Condition + expectation:* "Expired card is declined with recoverable error" |
| **Priority** | P1 (every build) / P2 (every release) / P3 (major releases) |
| **Technique** | EP / BVA / decision table / state transition / error guessing |
| **Requirement** | REQ-/story link |
| **Preconditions** | Logged-in state, cart contents, flags, seeded data |

## Steps

| # | Action | Expected result |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |

## Postconditions / cleanup
*State to reset (e.g., remove test order).*

## Execution record

| Date | Build | Result | Defect | Tester |
|---|---|---|---|---|
| | | ✅ Pass / ❌ Fail / ⚠️ Blocked | BUG- | |

---

### Rules of thumb
- One case = one condition = one verdict
- Expected results must be *checkable* — numbers, exact messages, exact states
- If a step needs a paragraph, it's probably two cases
