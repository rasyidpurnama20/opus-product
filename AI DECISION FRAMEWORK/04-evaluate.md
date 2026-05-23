# Stage 04 — Evaluate → Trade-off Matrix

**Code:** `EV` | **Output:** `TM-<decision-slug>-001`

## Purpose
Skor opsi dengan kriteria, transparan & dapat dipertanyakan. Bukan "feeling", tapi numerik.

## DoD
- [ ] Matrix: opsi × kriteria, skor 1–5 atau 1–10.
- [ ] Weighted score dihitung.
- [ ] **Premortem** untuk top 2: "kalau gagal di 6 bulan, alasannya apa?"
- [ ] Sensitivity check: ubah weight ±20%, apakah ranking berubah?

## Prompt
```
ROLE: analyst yang skeptis. Suka tantang skoring.
INPUT: OM + DC.
TASK:
- Skor tiap opsi vs tiap kriteria (1–5).
- Hitung weighted score.
- Top 2 → premortem (5 alasan kegagalan paling mungkin).
- Sensitivity: kalau weight kriteria #1 turun 20%, apakah ranking berubah? Kalau iya → keputusan rapuh.
OUTPUT: 04-tradeoff-matrix.md.
CONSTRAINTS: skor harus disertai 1 kalimat justifikasi.
ACCEPTANCE: matrix complete, premortem ada, sensitivity dicek.
```

## Template
```markdown
# Trade-off Matrix — {{title}}

| Field | Value |
|---|---|
| ID | TM-{{slug}}-001 |
| Linked OM, DC | OM-{{slug}}-001, DC-{{slug}}-001 |

## Matrix (raw 1–5)
| Criterion | Weight | Opt A | Opt B | Opt C | Opt D |
|---|---|---|---|---|---|
| C1 ACID + complex query | 35 | 5 | 2 | 5 | 4 |
| C2 horizontal scale | 25 | 3 | 4 | 4 | 4 |
| C3 ops effort | 15 | 2 | 4 | 3 | 5 |
| C4 cost yr | 15 | 5 | 4 | 4 | 3 |
| C5 hiring | 10 | 4 | 3 | 4 | 4 |

## Justifications
- Opt A — C1=5: native, mature; C3=2: backup/replication custom DIY.
- Opt B — C1=2: workaround for joins/transactions.
- Opt C — C1=5: distributed Postgres flavor.
- Opt D — C3=5: managed; C4=3: pricier per node.

## Weighted Score
| Option | Score |
|---|---|
| Opt A | 4.05 |
| **Opt C** | **4.20** |
| Opt D | 3.95 |
| Opt B | 3.10 |

## Premortem (top 2)

### Opt C (Citus / distributed Postgres)
6-month failure scenarios:
1. Sharding key salah → reshard mahal.
2. Tooling kurang matang dibanding vanilla PG.
3. Migration tidak smooth → downtime > SLA.
4. Talent: hard to hire someone yang familiar.
5. Vendor lock-in.

### Opt A (Postgres single-node)
6-month failure scenarios:
1. Vertical limit ketemu sebelum bisa migrasi.
2. Backup window > acceptable.
3. Read replica lag jadi bottleneck.

## Sensitivity Check
- Turunkan C1 weight 35→25 (anggap kurang penting): Opt C masih #1, gap menyempit.
- Turunkan C2 weight 25→15: Opt A naik ke #1 (4.10 vs 3.95).
- **Conclusion:** ranking sensitif ke "berapa penting horizontal scale" — keputusan tergantung pada keyakinan growth proyeksi.

## Recommendation
- Jika growth proyeksi ≥ 5× dalam 18 bulan → Opt C.
- Jika growth ≤ 3× → Opt A (lebih simple, terbukti, hindari kompleksitas premature).
```
