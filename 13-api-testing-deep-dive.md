# Stage 12 — API Testing Deep Dive

> **Goal:** go from "I can send a request in Postman" to owning API quality end-to-end: HTTP mastery, negative design, auth flows, contract testing, GraphQL, and automation-ready collections. API skill is the single biggest pay-rise lever for a manual tester.

## 1. HTTP fluency — the non-negotiable base

| Concept | What you must know cold |
|---|---|
| **Methods** | GET (read, idempotent) · POST (create) · PUT (replace) · PATCH (partial update) · DELETE — and *test that the API actually respects these semantics* |
| **Status codes** | 200/201/204 success family · 301/302 redirects · 400 bad request · 401 unauthenticated · 403 unauthorized · 404 not found · 409 conflict · 422 validation · 429 rate-limited · 500/502/503 server errors |
| **Headers** | `Content-Type`, `Authorization`, `Accept`, `Cache-Control`, CORS headers, custom `X-*` |
| **Idempotency** | Sending the same POST twice should NOT create two orders (remember the [double-charge bug](examples/sample-bug-report.md)?) — look for idempotency keys |

**Classic bugs to hunt:** wrong status code with right behavior (returns 200 with `{"error":...}` body — a lie), 500 where 400 belongs (unvalidated input reaching the server), 200 on someone else's resource (authorization hole — see [Security](14-security-testing.md)).

## 2. Designing API test cases (same craft, new surface)

Your [Stage 1 techniques](02-test-design-techniques.md) map directly. For `POST /bookings {checkin, checkout, guests}`:

| Technique | API test |
|---|---|
| EP | valid booking · missing required field · wrong type (`"guests": "two"`) · unknown extra field |
| BVA | guests: 0, 1, max, max+1 · checkout = checkin (same day allowed?) · checkin in the past |
| State | double-book the same room · cancel twice · modify a cancelled booking |
| Error guessing | huge payload · empty body `{}` · malformed JSON `{"checkin":` · SQL/script strings in text fields · duplicate keys in JSON |

**Response assertions — check all four layers every time:**
1. **Status code** is exactly right
2. **Body** — required fields present, correct types, correct *values*
3. **Headers** — content-type, no sensitive data leaking
4. **Side effects** — the DB row / follow-up GET / email actually reflects it

## 3. Postman like a professional

- **Collections as suites:** one folder per endpoint, ordered happy-path → negatives
- **Environments:** `dev` / `staging` with `{{base_url}}`, `{{token}}` — never hardcode
- **Pre-request scripts:** fetch a fresh auth token automatically
- **Tests tab (JavaScript):**

```javascript
pm.test("201 Created", () => pm.response.to.have.status(201));
pm.test("booking id returned", () => {
  const body = pm.response.json();
  pm.expect(body.bookingid).to.be.a("number");
});
pm.test("fast enough", () => pm.expect(pm.response.responseTime).to.be.below(800));
```

- **Collection Runner / Newman:** run the whole suite on demand or in CI — your manual collection becomes automation for free:

```bash
newman run booking-api.postman_collection.json -e staging.postman_environment.json
```

Free structured learning: [Postman Learning Center](https://learning.postman.com/) and the [freeCodeCamp Postman course](https://www.youtube.com/watch?v=VywxIQ2ZXw4).

## 4. Auth flows — where API testing gets real

| Auth type | What to test |
|---|---|
| **API keys** | Missing key → 401 · revoked key → 401 · key in URL (bad practice — flag it) |
| **Bearer / JWT** | Expired token → 401 · tampered signature → 401 · token from user A on user B's resource → 403/404 · decode the JWT ([jwt.io](https://jwt.io)) and check what's inside — PII in a JWT is a finding |
| **OAuth 2.0** | Know the authorization-code flow conceptually; test scope enforcement (read-only token attempting writes) |
| **Sessions/cookies** | Missing `HttpOnly`/`Secure` flags · session survives logout? · concurrent sessions policy |

## 5. Contract testing & OpenAPI

The **OpenAPI spec** (Swagger) is the API's contract. Contract testing = verifying the implementation matches it — and that changes don't break consumers.

- **Read the spec first, test against the spec, file spec-vs-reality gaps as bugs** — half of API bugs live in that gap
- Import the spec into Postman → instant request skeletons for every endpoint
- Validate responses against the schema (Postman can assert JSON schema; tools like **Spectral** lint the spec itself)
- Concept to know for interviews: **consumer-driven contracts (Pact)** — consumers publish what they rely on; providers verify against it in CI

## 6. GraphQL testing — the different beast

- One endpoint, many queries: test **over-fetching authorization** (can I query fields I shouldn't see?), **deep nesting** (10-level nested query — DoS vector), **batched mutations**
- Introspection: `__schema` queries reveal the whole API — should it be enabled in prod?
- Same negative discipline: wrong types in variables, missing required arguments, huge page sizes

## 7. Practice lab (free, safe, real)

| Target | Use it for |
|---|---|
| [restful-booker](https://restful-booker.herokuapp.com/apidoc/index.html) | Full CRUD + auth — deliberately buggy: find them |
| [ReqRes](https://reqres.in/) | Quick request practice |
| [JSONPlaceholder](https://jsonplaceholder.typicode.com/) | Fake data APIs |
| [Postman Echo](https://learning.postman.com/docs/developer/echo-api/) | Inspect exactly what you sent |
| [GoRest](https://gorest.co.in/) | Auth-token CRUD practice |
| [OWASP crAPI](https://github.com/OWASP/crAPI) | *Completely ridiculous API* — API security practice (pairs with next chapter) |

**Portfolio move:** a public Postman collection for restful-booker with 40+ requests covering all four assertion layers, negatives included, runnable via Newman — plus a README of the bugs you found. That artifact alone gets interviews.

## ✅ Exercise

Against restful-booker:
1. Create → read → update → delete a booking, asserting all four layers each step
2. Try updating a booking with an expired/invalid token — document exactly what happens vs what *should*
3. Send `{"firstname": "<script>alert(1)</script>"}` — is it stored? Echoed back raw? Where would that bite a consumer?

**Next →** [Stage 13: Security Testing](14-security-testing.md)
