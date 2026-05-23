# Stage 08 — Release

**Code:** `REL`
**Output Artifact:** Release Notes (`RN`) + Runbook (`RB`)

## Tujuan
Mengkomunikasikan apa yang dirilis ke user/stakeholder dan menyiapkan tim operasional untuk memantau & merespon insiden.

## Owner
Tech Lead + Product Manager. AI berperan sebagai *writer & checklist generator*.

## Input
- `TR-<feature>` (status `GO`).
- Daftar PR yang masuk rilis.
- `ARCH` + ADR untuk konteks operasional.

## Output
- `rn-<feature>-001.md` — Release Notes (audience: user / stakeholder).
- `rb-<feature>-001.md` — Runbook (audience: on-call / SRE):
  - Health check, dashboard link.
  - Common alarm + mitigation.
  - Rollback procedure.
  - Feature flag config.

## DoR
- [ ] Test Report `GO`.
- [ ] Semua bug `Critical` / `High` tertutup atau punya mitigasi.

## DoD
- [ ] Release Notes memuat: New, Changed, Fixed, Known Issues, Migration Guide.
- [ ] Runbook memuat: Health, Alerts, Rollback, Feature Flag, Contact.
- [ ] Tag rilis dibuat di repo (`vX.Y.Z`).
- [ ] Komunikasi ke user/stakeholder terkirim.

## Anti-Pattern
- Release Notes berisi jargon engineering.
- Runbook tanpa rollback procedure.
- Tidak ada feature flag untuk fitur berisiko.
