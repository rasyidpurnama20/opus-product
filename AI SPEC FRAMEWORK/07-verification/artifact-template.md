# Test Plan — {{Feature Name}}

| Field | Value |
|---|---|
| ID | `TP-{{feature-slug}}-001` |
| Status | `DRAFT` |
| Linked PRD | `PRD-{{feature-slug}}-001` |
| Linked US | `US-{{feature-slug}}-001` |

## 1. Scope
- **In:** {{...}}
- **Out:** {{...}}

## 2. Test Levels & Tools
| Level | Tool | Note |
|---|---|---|
| Unit | {{vitest/jest/pytest}} | per package |
| Integration | {{...}} | DB + API |
| Contract | {{schemathesis/dredd}} | vs OAS |
| E2E | {{playwright/cypress}} | critical path |
| Load | {{k6/locust}} | NFR latency |
| Security | {{zap/trivy}} | OWASP Top 10 |

## 3. Test Cases

### TC-{{feature-slug}}-001 — Happy path: create order
- **Linked AC:** `US-{{feature}}-001` Scenario "Happy path"
- **Level:** E2E
- **Pre-condition:** User logged in, cart contains 1 item.
- **Steps:**
  1. POST `/orders` with valid payload.
  2. GET `/orders/{id}`.
- **Expected:**
  - Step 1 returns 201, body matches `Order` schema, `status = pending`.
  - Step 2 returns 200, same `id`.

### TC-{{feature-slug}}-002 — Edge: empty cart
- **Linked AC:** `US-{{feature}}-001` Scenario "Edge case"
- ...

## 4. Test Data
- {{seed plan, fixture}}.

## 5. Environment
- {{staging URL, kredensial test, observability}}.

## 6. Exit Criteria
- 100% TC pass atau bug yang gagal sudah ditriase ke severity ≤ Low.
- NFR target tercapai.

---

# Test Report — {{Feature Name}}

| Field | Value |
|---|---|
| ID | `TR-{{feature-slug}}-001` |
| Linked TP | `TP-{{feature-slug}}-001` |
| Build | {{commit sha / version}} |
| Run Date | {{YYYY-MM-DD}} |

## 1. Summary
| Metric | Value |
|---|---|
| Total TC | 24 |
| Passed | 23 |
| Failed | 1 |
| Skipped | 0 |

## 2. Result Detail
| TC ID | Result | Note |
|---|---|---|
| TC-001 | PASS | |
| TC-002 | FAIL | Bug-007 |

## 3. NFR Result
| NFR | Target | Actual | Status |
|---|---|---|---|
| NFR-001 latency p95 | < 300ms | 245ms | PASS |
| NFR-002 uptime | 99.9% | n/a | DEFERRED |

## 4. Bugs Opened
| ID | Severity | Title | Linked TC |
|---|---|---|---|
| BUG-007 | Medium | Negative quantity accepted | TC-002 |

## 5. Decision
- **Go / No-Go:** {{GO}} \| {{NO-GO}}
- **Reason:** {{...}}
- **Mitigation if GO:** {{...}}
