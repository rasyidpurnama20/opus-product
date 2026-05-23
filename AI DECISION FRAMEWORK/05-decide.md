# Stage 05 — Decide → Decision Record

**Code:** `DC` | **Output:** `DR-<decision-slug>-001`

## Purpose
Tegas memutuskan, dokumentasikan supaya konsisten dan bisa di-trace.

## DoD
- [ ] DR: decision tegas (1 kalimat), reasoning singkat, expected outcome, kill criteria, owner, review date.
- [ ] Komunikasi keluar (announce ke stakeholder).

## Prompt
```
ROLE: decision maker yang menulis decision record (ADR-style).
INPUT: TM hasil + sensitivity analysis.
TASK:
- Tulis 1 kalimat keputusan tegas.
- Reasoning 3–5 bullet (tanpa hedging).
- Expected outcome dalam 3, 6, 12 bulan (observable).
- Kill criteria: kondisi apa yang akan membuat kita revisit/revert.
- Komunikasi: siapa yang harus tahu, format apa.
OUTPUT: 05-decision-record.md.
CONSTRAINTS: hindari "we'll see", "kind of"; tegas.
ACCEPTANCE: decision tegas, kill criteria eksplisit, owner & date.
```

## Template
```markdown
# Decision Record — {{title}}

| Field | Value |
|---|---|
| ID | DR-{{slug}}-001 |
| Status | DECIDED |
| Date | {{...}} |
| Owner | {{...}} |
| Review on | {{date 6 months later}} |

## Decision
> Kami memilih **Opt A (Postgres single-node managed)** untuk analytics service.

## Reasoning
- Trade-off matrix gap kecil (4.05 vs 4.20), sensitivity check menunjukkan kerentanan ranking ke asumsi growth.
- Konservatisme: growth proyeksi 18 bulan tidak konfirmatif, mulai dengan vanilla PG menghindari premature complexity.
- Opsi A reversible: migrasi ke Citus / distributed kelak feasible.
- Tim familiar; deliverable lebih cepat.

## Expected Outcome
- 3 bulan: service jalan, p99 read < 200ms pada load saat ini.
- 6 bulan: capacity headroom ≥ 50%.
- 12 bulan: keputusan revisit jika query throughput > 80% capacity OR storage > 70%.

## Kill Criteria (revisit / revert)
- Throughput sustained > 80% selama 4 minggu.
- Storage projection ke 12 bulan > 70%.
- Backup window > 1 jam untuk recovery point objective.
- Read replica lag > 5 detik p99 untuk 1 jam.

## Communication Plan
- Engineering all-hands: 5 min recap.
- Slack #engineering: pin link DR.
- Document in `docs/adr/`.
- Onboarding doc updated.

## Sign-off
- {{name}}, {{role}}, date.
```
