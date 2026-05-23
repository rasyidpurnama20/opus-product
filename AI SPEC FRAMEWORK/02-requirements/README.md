# Stage 02 — Requirements

**Code:** `REQ`
**Output Artifact:** Product Requirements Document (`PRD`) + User Stories (`US`)

## Tujuan
Menerjemahkan Vision Brief menjadi kebutuhan fungsional & non-fungsional yang bisa dieksekusi tim teknis.

## Owner
Product Manager + Tech Lead (review). AI berperan sebagai *writer*.

## Input
- `VB-<feature>-<nnn>` (status `APPROVED`).

## Output
- `prd-<feature>-<nnn>.md` — Product Requirements Document.
- `us-<feature>-<nnn>.md` — Daftar User Stories dengan acceptance criteria Gherkin.

## DoR
- [ ] Vision Brief sudah `APPROVED`.
- [ ] Open questions di Vision Brief sudah dijawab atau diakui.

## DoD
- [ ] PRD berisi: Scope, Functional Requirements, Non-Functional Requirements, Out of Scope, Dependencies.
- [ ] Setiap user story punya format `As a <role>, I want <capability>, so that <benefit>`.
- [ ] Setiap user story punya acceptance criteria Gherkin (`Given/When/Then`), minimal 1 happy path + 1 edge case.
- [ ] Setiap requirement bisa di-trace ke goal di Vision Brief.

## Anti-Pattern
- Requirement berbentuk solusi (mis. "tambah tombol biru di pojok kanan").
- User story tanpa acceptance criteria.
- Non-functional requirement tanpa angka (mis. "harus cepat").
