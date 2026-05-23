# Prompt — Stage 07 Verification → Test Plan + Test Report

## 1. ROLE
You are a **Senior QA Engineer** with strong skills in test design (boundary, equivalence, exploratory) and load testing.

## 2. CONTEXT
{{deskripsi sistem & lingkungan test (staging URL, data seed, dst).}}

## 3. INPUT ARTIFACT(S)
- `US-{{feature}}-001` (acceptance criteria Gherkin):
```
{{paste}}
```
- `PRD-{{feature}}-001` NFR:
```
{{paste tabel NFR}}
```
- `OAS-{{feature}}-001`: {{paste / link}}

## 4. TASK
Hasilkan **dua artifact**:

### A. Test Plan (`tp-{{feature}}-001.md`)
- Scope (in/out).
- Test levels: Unit, Integration, Contract (vs OAS), E2E, Load, Security.
- Test cases dengan ID `TC-{{feature}}-NNN`. Setiap TC punya: prasyarat, langkah, expected result, linked AC.
- Test data plan.
- Environment plan.
- Exit criteria.

### B. Test Report (`tr-{{feature}}-001.md`) (template kosong dulu, diisi setelah eksekusi)
- Run summary (date, build).
- Pass/Fail per TC.
- Bug list (dengan severity).
- NFR result (latency p95, error rate, dst).
- Go/No-Go decision + alasan.

## 5. OUTPUT ARTIFACT
- `tp-{{feature}}-001.md`
- `tr-{{feature}}-001.md`
- Template: `./artifact-template.md`.

## 6. CONSTRAINTS
- Setiap acceptance criteria Gherkin **wajib** punya minimal 1 TC.
- Setiap NFR dengan target numerik **wajib** punya TC load/perf.
- Endpoint di OAS **wajib** punya contract test.

## 7. ACCEPTANCE CRITERIA
- [ ] Coverage AC ↔ TC = 100%.
- [ ] Coverage NFR ↔ TC = 100% (yang punya angka).
- [ ] Setiap TC punya expected result yang spesifik (bukan "berhasil").
- [ ] Test Report punya format Go/No-Go.
