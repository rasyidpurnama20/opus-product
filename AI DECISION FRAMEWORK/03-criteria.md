# Stage 03 — Criteria → Decision Criteria

**Code:** `CR` | **Output:** `DC-<decision-slug>-001`

## Purpose
Tetapkan kriteria & bobot **sebelum** lihat skor opsi. Kalau dibalik, kriteria akan bias mengikuti opsi favorit.

## DoD
- [ ] DC memuat: 4–7 kriteria yang independen, definisi terukur, bobot total = 100, sumber kepentingan tiap kriteria.

## Prompt
```
ROLE: framework decision-maker.
INPUT: DB-{{slug}}-001.
TASK:
- Sarankan 4–7 kriteria yang relevan untuk keputusan ini.
- Definisikan tiap kriteria measurably (mis. "biaya 1 tahun" bukan "murah").
- Beri bobot, total = 100. Justifikasi bobot.
- Pastikan kriteria independen (tidak overlap).
- Ada minimal 1 kriteria "opportunity cost" (apa yang dikorbankan).
OUTPUT: 03-decision-criteria.md.
CONSTRAINTS: definisi terukur. Bobot harus 100.
ACCEPTANCE: 4+ kriteria measurable, bobot=100, justifikasi.
```

## Template
```markdown
# Decision Criteria — {{title}}

| Field | Value |
|---|---|
| ID | DC-{{slug}}-001 |
| Linked DB | DB-{{slug}}-001 |

## Criteria
| ID | Criterion | Definition | Weight | Why this weight |
|---|---|---|---|---|
| C1 | Query power (ACID + complex query) | Mendukung join, transaction, complex aggregation | 35 | core need analitik |
| C2 | Horizontal scalability | Bisa scale to 10× data dalam 2 tahun | 25 | proyeksi growth |
| C3 | Operational effort | Manhour/bulan untuk maintain | 15 | tim kecil |
| C4 | Cost (1y total) | Infra + license $/yr | 15 | budget terbatas |
| C5 | Hiring & ramp | Mudah hire / ramp engineer | 10 | turnover risk |
| **Total** | | | **100** | |

## Notes
- C1 + C2 conflict potential (ACID-compliant horizontal scale susah). Tradeoff disengaja.
- C3 dan C4 tidak overlap: C3 manhour, C4 dollar.
- Tidak ada kriteria "ego/popularity" — sengaja dihindari.
```
