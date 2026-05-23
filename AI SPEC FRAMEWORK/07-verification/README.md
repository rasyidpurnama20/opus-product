# Stage 07 — Verification

**Code:** `VER`
**Output Artifact:** Test Plan (`TP`) + Test Report (`TR`)

## Tujuan
Membuktikan bahwa implementasi memenuhi acceptance criteria dari user stories dan NFR dari PRD.

## Owner
QA Engineer / Engineer. AI berperan sebagai *test designer & report writer*.

## Input
- `US-<feature>` + acceptance criteria Gherkin.
- `PRD-<feature>` (untuk NFR target).
- Source code hasil stage 06.
- `OAS-<feature>` (kontrak API yang harus diuji).

## Output
- `tp-<feature>-001.md` — Test Plan: scope, level (unit/integration/e2e/load/security), test cases, data, environment.
- `tr-<feature>-001.md` — Test Report: hasil eksekusi (pass/fail), bug, coverage.

## DoR
- [ ] Implementation `T-*` task `IN_REVIEW`.
- [ ] Acceptance criteria user stories tersedia.

## DoD
- [ ] Setiap acceptance criteria Gherkin punya minimal 1 test case di Test Plan.
- [ ] NFR yang punya angka target (latency, throughput) punya test plan-nya (load test).
- [ ] Test Report mencantumkan hasil eksekusi terbaru, bug terbuka, dan keputusan go/no-go.

## Anti-Pattern
- Test plan hanya happy path.
- Tidak ada load test padahal NFR punya target latency.
- Test report tanpa go/no-go decision.
