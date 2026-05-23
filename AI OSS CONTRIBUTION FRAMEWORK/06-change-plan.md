# Stage 06 — Change Plan → Change Plan

**Code:** `CP` | **Output:** `CP-<repo>-<issue#>`

## Purpose
Menetapkan **rencana perubahan minimal** sebelum coding. Banyak PR ditolak karena scope creep — Change Plan mencegah ini.

## DoR
- [ ] Repro Report (untuk bug) atau Issue Brief lengkap (untuk feature).

## DoD
- [ ] Daftar file yang akan disentuh & sifat perubahan (add / modify / delete).
- [ ] 2–3 alternatif pendekatan dengan trade-off.
- [ ] Pendekatan terpilih + alasan.
- [ ] Test plan (test mana yang ditambah/diubah).
- [ ] Risiko & mitigasi.

---

## Prompt Template

```
1. ROLE
You are a tech lead reviewing a contributor's change plan before they code.
You optimise for: smallest diff that solves the issue, in repo's house style.

2. CONTEXT
Saya akan implement {{issue#}} di {{repo}}.

3. INPUT
- IB-{{repo}}-{{issue#}}: {{paste}}
- RR-{{repo}}-{{issue#}} (kalau bug): {{paste}}
- CM-{{repo}}-001 (relevant section): {{paste relevan}}

4. TASK
- Identifikasi 2–3 alternatif pendekatan (mis. fix di lapis A vs B vs C).
- Per alternatif: file yang disentuh, kompleksitas, risiko, backward compatibility.
- Rekomendasikan satu, jelaskan alasannya.
- Plan test: unit/integration/e2e mana yang ditambah/dimodifikasi.
- Identifikasi risiko + mitigasi.
- Sketch commit plan (1–N commits, atomik).

5. OUTPUT
06-change-plan-{{issue#}}.md.

6. CONSTRAINTS
- Pilih solusi termurah (smallest diff, maintain backward compat) kecuali ada alasan kuat.
- Tidak menambah dependency baru kecuali sangat perlu (dan Anda akan justify di PR).

7. ACCEPTANCE
- [ ] 2–3 alternatif terdokumentasi.
- [ ] Test plan eksplisit.
- [ ] Commit plan atomik.
```

---

## Artifact Template — `CP-<repo>-<issue#>`

```markdown
# Change Plan — {{owner/repo}}#{{issue#}}

| Field | Value |
|---|---|
| ID | CP-{{repo-slug}}-{{issue#}} |
| Status | DRAFT |
| Linked IB | IB-{{repo-slug}}-{{issue#}} |
| Linked RR | RR-{{repo-slug}}-{{issue#}} |

## 1. Problem Recap (1 paragraf)
{{...}}

## 2. Alternatives

### A. Fix at validator layer
- **Files:** `src/middleware/validate.ts`, `src/types.ts`.
- **Diff size:** ~30 LOC.
- **Pro:** localized, no behavior change for other endpoints.
- **Con:** doesn't help future endpoints with same pattern.
- **BC:** safe.

### B. Fix at controller layer
- **Files:** `src/users/controller.ts`.
- **Diff size:** ~10 LOC.
- **Pro:** smallest.
- **Con:** root cause (uncaught error) tetap.
- **BC:** safe.

### C. Add global error handler
- **Files:** `src/server.ts`, plus 12 controllers to remove ad-hoc.
- **Diff size:** ~150 LOC.
- **Pro:** systemic.
- **Con:** big PR, scope creep, will be rejected.
- **BC:** behavior change — risky.

## 3. Chosen Approach
**A**, with note in PR description that B/C considered.

Reason: smallest meaningful fix, addresses root cause within one module, keeps PR reviewable.

## 4. Files to Touch
| File | Change | Note |
|---|---|---|
| `src/middleware/validate.ts` | modify | wrap call in try-catch, return 422 on Joi/Zod throw |
| `src/types.ts` | add | union `ValidationError` type |
| `tests/middleware/validate.test.ts` | add | 3 cases |

## 5. Test Plan
- Unit: validator catches schema error → 422 (not 500).
- Unit: validator passes through unrelated errors.
- Regression: existing 412-passing test suite stays green.

## 6. Risks
| Risk | Mitigation |
|---|---|
| Some controller relied on 500 to trigger retry middleware | Audit usages; doc note in PR. |
| Error message reveals schema | Sanitize message in test. |

## 7. Commit Plan
1. `test(validate): add failing tests for uncaught throw` (TDD).
2. `fix(validate): catch validator throw and return 422`.
3. `docs(error): note 422 vs 500 for validation`.

## 8. Out of Scope (mention in PR)
- Refactor controllers to use global error handler — separate PR.
- Sanitize error message format — separate PR.
```
