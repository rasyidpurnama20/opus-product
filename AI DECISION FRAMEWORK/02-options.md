# Stage 02 — Options → Options Map

**Code:** `OP` | **Output:** `OM-<decision-slug>-001`

## Purpose
Generate **lebih dari 2** opsi (termasuk yang ekstrem) supaya ruang keputusan tidak sempit.

## DoD
- [ ] OM memuat: ≥ 3 opsi, deskripsi tiap, level of effort, status quo, "do nothing" eksplisit, opsi ekstrem (status quo, all-in, hybrid, defer).

## Prompt
```
ROLE: divergent thinker yang generate opsi tanpa filter dulu.
INPUT: DB-{{slug}}-001.
TASK:
- Generate ≥ 5 opsi (boleh aneh):
  1. Status quo (do nothing).
  2. Conservative.
  3. Balanced.
  4. Aggressive.
  5. Opsi out-of-the-box yang tidak dipikir biasanya.
- Untuk masing-masing: deskripsi 2 kalimat, effort (S/M/L/XL), risiko utama, biaya kasar.
OUTPUT: 02-options-map.md.
CONSTRAINTS: tidak boleh skor / pilih dulu. Hanya generate.
ACCEPTANCE: ≥ 5 opsi, status quo termasuk, opsi ekstrem ada.
```

## Template
```markdown
# Options Map — {{title}}

| Field | Value |
|---|---|
| ID | OM-{{slug}}-001 |
| Linked DB | DB-{{slug}}-001 |

## Options

### A. Status quo (do nothing)
- Tetap pakai MongoDB.
- Effort: S.
- Risk: bottleneck makin parah, tech debt menumpuk.
- Cost: $0 sekarang, $$$$ kelak.

### B. Migrate to Postgres
- Pindah ke PG single-node managed (RDS / Aurora).
- Effort: L (10–14 weeks).
- Risk: migration data integrity, downtime.
- Cost: $$$ infra, dev time L.

### C. Migrate to distributed Postgres (Citus / CockroachDB)
- Distributed PG flavor.
- Effort: XL.
- Risk: complexity, talent.
- Cost: $$$$.

### D. Augment Mongo with Materialized Views
- Pakai Mongo aggregation framework + pre-computed views.
- Effort: M.
- Risk: tetap kena ceiling Mongo untuk analitik berat.
- Cost: $.

### E. Add separate analytics DB (ClickHouse / DuckDB)
- Mongo as OLTP, ClickHouse as OLAP.
- Effort: L.
- Risk: dual-DB ops complexity.
- Cost: $$.

### F. Defer 6 months, gather more data
- Tunggu Q4 review.
- Effort: S.
- Risk: kalau bottleneck akut, terlambat.
- Cost: $.

## Eliminated Quickly (with reason)
- (none yet — eliminate at stage 04 only)
```
