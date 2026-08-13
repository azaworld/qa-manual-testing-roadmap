# Stage 1 — Test Design Techniques

> **Goal:** design the *fewest* tests that find the *most* bugs. This is the craft that separates professionals from button-clickers.

Running example throughout: **an age field that accepts 18–60 (inclusive) for an insurance signup.**

## 1. Equivalence Partitioning (EP)

Split inputs into groups (*partitions*) where the system should behave the same. Test **one value per partition** — if 25 works, 26–59 almost certainly work too.

For the age field:

| Partition | Range | Test value | Expected |
|---|---|---|---|
| Invalid — too low | < 18 | 10 | Rejected with clear message |
| **Valid** | 18–60 | 35 | Accepted |
| Invalid — too high | > 60 | 75 | Rejected with clear message |
| Invalid — not a number | text, symbols | `abc`, `!@#` | Rejected, no crash |
| Invalid — empty | blank | `""` | Required-field message |

**5 tests instead of hundreds.** That's the point.

## 2. Boundary Value Analysis (BVA)

Bugs love edges — developers write `>` when they mean `>=`. Test **on and around every boundary**:

For 18–60: test **17, 18, 19** and **59, 60, 61**.

| Value | Expected | Why |
|---|---|---|
| 17 | Reject | Just below lower boundary |
| 18 | Accept | Exactly on lower boundary ← most common bug site |
| 19 | Accept | Just above lower boundary |
| 59 | Accept | Just below upper boundary |
| 60 | Accept | Exactly on upper boundary ← second most common bug site |
| 61 | Reject | Just above upper boundary |

**EP + BVA together** is your default for any input field, price range, date range, file-size limit, or pagination.

## 3. Decision Table Testing

For business rules with **multiple conditions combining**. Example: free-shipping rules —

*Free shipping if: order ≥ $50 AND member, OR any order with a FREESHIP coupon.*

| Rule | Order ≥ $50? | Member? | Coupon? | → Free shipping? |
|---|:---:|:---:|:---:|:---:|
| R1 | Y | Y | N | ✅ Yes |
| R2 | Y | N | N | ❌ No |
| R3 | N | Y | N | ❌ No |
| R4 | N | N | N | ❌ No |
| R5 | N | N | Y | ✅ Yes |
| R6 | Y | Y | Y | ✅ Yes (no double discount?) ← **ask the PM!** |

Decision tables **expose requirement gaps** (R6) before a single test runs. This is where manual QA earns respect.

## 4. State Transition Testing

For anything with **states and rules about moving between them** — orders, user accounts, documents.

Example: account lockout (3 failed logins → locked):

```
[Active] --wrong pwd--> [1 fail] --wrong pwd--> [2 fails] --wrong pwd--> [LOCKED]
   ^                        |                       |
   +----correct pwd---------+-----correct pwd-------+        [LOCKED] --reset link--> [Active]
```

Test every **valid transition** (correct password at 2 fails → Active) and every **invalid one** (correct password while LOCKED must NOT unlock).

## 5. Pairwise (Combinatorial) Testing

When configs explode: 3 browsers × 3 OSes × 2 user types = 18 combos. Most bugs involve **interactions of just two factors**, so cover every *pair* instead of every *combination* — tools like [pairwise.dev](https://pairwise.dev) or PICT generate a minimal set (usually ~9 instead of 18, or 50 instead of 5,000).

## 6. Error Guessing & Experience-Based Testing

The senior tester's secret weapon — a mental library of "what usually breaks":

- Paste emoji / RTL text / `<script>alert(1)</script>` into text fields
- Double-click the submit button fast (double-charge bugs — I've found these in **payment systems**)
- Hit back after checkout; refresh mid-payment
- Upload a 0-byte file, a 5GB file, a `.exe` renamed to `.jpg`
- Change timezone/locale; test around midnight and month-end
- Slow network (throttle in DevTools), then kill the connection mid-request

## 7. Exploratory Testing — structured, not random

Exploratory ≠ aimless clicking. Use **charters** and **time-boxes**:

> **Charter:** Explore *the coupon flow* with *stacked and expired coupons* to discover *pricing errors*. **Time-box:** 45 min. **Log:** what you tried, what surprised you, bugs found.

A session that finds nothing still produces knowledge: "coupon flow is solid under these attacks."

## ✅ Exercise

Design tests for a **password reset flow** (email link, expires in 30 min, single-use):
1. EP + BVA on the expiry (29 min, 30 min, 31 min)
2. State transitions (used link, expired link, second request invalidating the first?)
3. Five error-guessing attacks

Compare with [the worked checkout example](examples/ecommerce-checkout-test-cases.md).

**Next →** [Stage 2: Test Artifacts](03-test-artifacts.md)
