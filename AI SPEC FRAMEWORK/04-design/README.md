# Stage 04 — Design

**Code:** `DES`
**Output Artifact:** Data Model (`DM`) + OpenAPI Spec (`OAS`) + UI Spec (`UIS`)

## Tujuan
Mendetilkan kontrak yang dipakai semua layer: data, API, dan UI. Output stage ini adalah *acuan implementasi* yang siap di-generate jadi kode.

## Owner
Tech Lead (DM, OAS) + Designer/PM (UIS). AI berperan sebagai *drafter*.

## Input
- `ARCH-<feature>` + ADRs `APPROVED`.
- `US-<feature>`.

## Output
- `dm-<feature>-001.md` — Entity, atribut, relasi, constraint, indexing strategy.
- `oas-<feature>-001.yaml` — OpenAPI 3.1 spec (paths, schemas, security).
- `uis-<feature>-001.md` — Daftar screen, state, komponen, copy, error states.

## DoR
- [ ] Architecture Doc + ADR `APPROVED`.

## DoD
- [ ] Data Model lengkap untuk seluruh user story di scope.
- [ ] OpenAPI spec valid (lulus linter spectral/redocly).
- [ ] UI Spec memuat semua state: loading, empty, error, success.
- [ ] Setiap user story bisa dipenuhi oleh kombinasi DM + OAS + UIS.

## Anti-Pattern
- API endpoint tanpa schema response.
- Data model tanpa primary key/index strategy.
- UI Spec hanya gambar tanpa state handling.
