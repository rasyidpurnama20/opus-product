# Product Requirements Document — {{Feature Name}}

| Field | Value |
|---|---|
| ID | `PRD-{{feature-slug}}-001` |
| Status | `DRAFT` |
| Version | `0.1.0` |
| Linked Vision Brief | `VB-{{feature-slug}}-001` |
| Author | {{nama}} |
| Date | {{YYYY-MM-DD}} |

## 1. Scope
{{Apa yang dibangun di iterasi ini.}}

## 2. Functional Requirements
| ID | Requirement | Linked Goal |
|---|---|---|
| FR-001 | {{...}} | G1 |
| FR-002 | | |

## 3. Non-Functional Requirements
| ID | Category | Requirement | Target |
|---|---|---|---|
| NFR-001 | Performance | API latency p95 | < 300 ms |
| NFR-002 | Availability | Monthly uptime | ≥ 99.9% |
| NFR-003 | Security | Auth method | OAuth 2.1 |

## 4. Out of Scope
- {{...}}

## 5. Dependencies
- {{tim, sistem, pihak ketiga}}

## 6. Traceability
| FR/NFR | Linked VB Goal |
|---|---|
| FR-001 | G1 |
| NFR-001 | G2 |

---

# User Stories — {{Feature Name}}

| Field | Value |
|---|---|
| ID | `US-{{feature-slug}}-001` (file ini menampung semua story fitur) |
| Status | `DRAFT` |
| Linked PRD | `PRD-{{feature-slug}}-001` |

## US-{{feature-slug}}-001
**As a** {{role}}, **I want** {{capability}}, **so that** {{benefit}}.

**Linked FR:** `FR-001`

**Acceptance Criteria:**

```gherkin
Scenario: Happy path - {{nama scenario}}
  Given {{kondisi awal}}
  When {{aksi}}
  Then {{hasil yang diharapkan}}

Scenario: Edge case - {{nama scenario}}
  Given {{kondisi awal}}
  When {{aksi}}
  Then {{hasil yang diharapkan}}
```

## US-{{feature-slug}}-002
{{...}}
