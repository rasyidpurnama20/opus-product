# Stage 06 — Review → Decision Retrospective

**Code:** `RV` | **Output:** `DRT-<decision-slug>-001`

## Purpose
Cek apakah keputusan tetap valid setelah waktu berjalan (target review date di DR). Hindari "set and forget".

## DoD
- [ ] DRT: outcome aktual vs expected, kill-criteria status, lessons learned, lanjut/revisit/revert.

## Prompt
```
ROLE: retrospektif coach.
INPUT: DR + data 6 bulan terakhir (metric, incident).
TASK:
- Bandingkan expected outcome vs actual.
- Cek tiap kill criterion: tercapai? mendekati?
- Lessons: asumsi mana yang ternyata salah?
- Verdict: CONTINUE / REVISIT / REVERT.
OUTPUT: 06-decision-retrospective.md.
ACCEPTANCE: data per criterion, verdict tegas.
```

## Template
```markdown
# Decision Retrospective — {{title}}

| Field | Value |
|---|---|
| ID | DRT-{{slug}}-001 |
| Linked DR | DR-{{slug}}-001 |
| Review date | {{6 months after decision}} |

## Outcome vs Expected
| Metric | Expected | Actual | Verdict |
|---|---|---|---|
| p99 read latency | < 200ms | 145ms | ✅ |
| Throughput headroom (6m) | ≥ 50% | 62% | ✅ |
| Migration cost (FE) | low | low | ✅ |

## Kill Criteria Status
| Criterion | Status |
|---|---|
| Throughput sustained > 80% | NO (peak 55%) |
| Storage 12m projection > 70% | NO (45%) |
| Backup window > 1h RPO | NO |
| Replica lag > 5s p99 | NO |

## Lessons Learned
- Asumsi growth 5× ternyata 2.3× — lebih lambat dari ekspektasi.
- Postgres managed ops effort lebih murah dari ekspektasi (-30%).
- Surprise: 1 endpoint analytics agregasi lambat → solved with materialized view.

## Verdict
**CONTINUE.** Tidak ada kill criteria triggered, semua expected outcome terlampaui. Re-review in 12 months.

## Updates to Decision Record
- DR-{{slug}}-001 status remained APPROVED.
- Added note: "growth proyeksi diperbarui ke 2× per tahun dari 5×".
- Next review: {{12 months later}}.
```
