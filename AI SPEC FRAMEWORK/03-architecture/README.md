# Stage 03 — Architecture

**Code:** `ARC`
**Output Artifact:** Architecture Document (`ARCH`) + Architecture Decision Records (`ADR`)

## Tujuan
Memutuskan struktur sistem tingkat tinggi: komponen, interaksi, batasan teknologi, dan trade-off, *sebelum* desain detail data/API/UI.

## Owner
Tech Lead / Solution Architect. AI berperan sebagai *drafter & analyst alternatif*.

## Input
- `PRD-<feature>` (status `APPROVED`).
- `US-<feature>` (status `APPROVED`).
- Existing system context: arsitektur saat ini, konstrain platform.

## Output
- `arch-<feature>-001.md` — gambaran arsitektur (komponen, alur data, integrasi).
- `adr-<feature>-NNN.md` — satu ADR per keputusan signifikan (database, framework, pola integrasi, dst).

## DoR
- [ ] PRD & User Stories `APPROVED`.
- [ ] NFR sudah jelas (krn menentukan pilihan arsitektur).

## DoD
- [ ] Architecture Doc memuat: System Context, Component View, Data Flow, Tech Stack, NFR Strategy, Risks.
- [ ] Setiap keputusan teknologi besar punya ADR sendiri (Context, Options, Decision, Consequences).
- [ ] Setiap NFR di PRD punya strategi pemenuhan yang dapat diidentifikasi di Architecture Doc.

## Anti-Pattern
- ADR tanpa "alternatif yang ditolak".
- Arsitektur "ikut tren" tanpa justifikasi NFR.
- Diagram tanpa narasi.
