# Stage 07 — Results → Results Pack

**Code:** `RS` | **Output:** `RPK-<paper-slug>-001`

## Purpose
Mengumpulkan **angka mentah dan figur** dengan disiplin: tracked, versioned, statistically honest. Tidak ada "perbaiki nanti pas drafting".

## DoR
- [ ] Codebase reproducible siap, run sudah jalan.

## DoD
- [ ] Results Pack berisi: tabel headline (mean ± std, p-value), tabel ablation, figur kunci (loss curves, scaling, ablation visualisasi), raw artifacts (CSV/JSON), provenance log (code commit, data version, seed, config).

---

## Prompt Template

```
1. ROLE
You are a results curator. You don't write narrative — you organize numbers honestly.

2. CONTEXT
Run sudah selesai. Saya butuh kompilasi result yang siap masuk paper.

3. INPUT
- EP-{{slug}}-001: {{paste}}
- Hasil mentah: {{path csv / wandb run ids}}
- Metric library yang dipakai: {{...}}

4. TASK
- Buat tabel headline: model × dataset × metric (mean ± std).
- Tambah significance test (paired t-test atau bootstrap CI 95%) untuk klaim utama.
- Buat ablation table per RQ.
- Sketsa figur:
  - Loss curve per model.
  - Scaling: metric vs param/seq-length.
  - Ablation heatmap.
  - Failure case examples.
- Catat provenance: commit, config hash, seed, run id.
- Flag anomalies (run yang outlier, failed run).

5. OUTPUT
07-results-pack.md + folder results/.

6. CONSTRAINTS
- TIDAK boleh cherry-pick seed.
- Outlier dilaporkan, bukan dihapus diam-diam.
- Setiap angka punya provenance trail.

7. ACCEPTANCE
- [ ] Headline table dengan std + significance.
- [ ] ≥ 1 ablation table per RQ.
- [ ] ≥ 4 figur dengan caption.
- [ ] Provenance log lengkap.
```

---

## Artifact Template — `RPK-<paper-slug>-001`

```markdown
# Results Pack — {{Working Title}}

| Field | Value |
|---|---|
| ID | RPK-{{slug}}-001 |
| Status | DRAFT |
| Linked EP | EP-{{slug}}-001 |
| Code commit (results frozen) | {{sha}} |

## 1. Headline Table
| Model | Dataset | Metric (mean ± std, n=5) | Δ vs ours | p-value (paired t) |
|---|---|---|---|---|
| Transformer | LRA | 53.4 ± 0.5 | -6.7 | < 0.001 |
| Mamba | LRA | 60.1 ± 0.3 | 0.0 | — |
| Performer | LRA | 51.4 ± 0.6 | -8.7 | < 0.001 |
| **Hybrid-AS (ours)** | LRA | **60.6 ± 0.2** | +0.5 | 0.04 |

## 2. Per-Dataset Tables
{{...detail per dataset...}}

## 3. Ablation Tables

### A1 — Layer Interleave Ratio (r)
| r | LRA acc | PPL | latency (ms) | memory (GB) |
|---|---|---|---|---|
| 2 | 60.1 ± 0.4 | 17.6 | 22 | 24 |
| **4** | **60.6 ± 0.2** | **17.4** | 18 | 19 |
| 8 | 59.8 ± 0.3 | 17.7 | 14 | 14 |

### A2 — Window × Stride
{{...heatmap data...}}

## 4. Figures

| # | Figure | File | Caption |
|---|---|---|---|
| 1 | Loss curves (5 seeds × 4 models) | `fig/loss_curves.pdf` | "Training loss; shading = ±1 std over 5 seeds." |
| 2 | Scaling: acc vs sequence length | `fig/scaling_seq.pdf` | "Accuracy vs sequence length 4k–32k. Hybrid maintains slope; full-attention OOM at 16k." |
| 3 | Ablation heatmap (W × S) | `fig/ablation_ws.pdf` | "Window size W and stride S; warmer = higher LRA acc." |
| 4 | Failure cases | `fig/failures.pdf` | "Examples where hybrid underperforms full-attention; pattern: exact retrieval." |

## 5. Provenance Log
| Result | Run ID | Commit | Config | Seed | Hardware | Date |
|---|---|---|---|---|---|---|
| Headline Hybrid LRA | wandb/abc123 | a1b2c3d | configs/exp/headline.yaml | 0 | 8×A100 80GB | 2026-04-12 |
| ... | | | | | | |

## 6. Anomalies & Notes
- Run `wandb/xyz789` (Hybrid seed=2) had NaN at step 14k → restarted from step 13k checkpoint with same seed → same final result; logged.
- Performer baseline at seq=32k OOM on 80GB; reported with `OOM`.

## 7. Raw Artifacts (in repo)
```
results/
├── headline.csv
├── ablation/
│   ├── layer_ratio.csv
│   ├── window_stride.csv
│   └── seq_length.csv
├── figures/
│   ├── loss_curves.pdf
│   └── ...
└── provenance.json
```
```
