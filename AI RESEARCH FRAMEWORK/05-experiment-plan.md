# Stage 05 — Experiment Plan → Experiment Plan

**Code:** `EP` | **Output:** `EP-<paper-slug>-001`

## Purpose
Menyusun **protokol eksperimen** yang lengkap: dataset versions, splits, metrics, baselines, ablations, seeds, hyperparameter, compute budget. Reviewer Q1 akan men-stress test ini.

## DoR
- [ ] Method Design `APPROVED`.

## DoD
- [ ] Experiment Plan memuat: dataset list (split + version), metric definition, baseline list (+ how reproduced), ablations (matrix), seeds policy (≥ 3), hyperparameter table, compute budget, eval protocol, fairness check.

---

## Prompt Template

```
1. ROLE
You are a rigorous experimentalist. You design protocols reviewers can't punch holes in.

2. CONTEXT
Method sudah jelas. Sekarang protokol eksperimen.

3. INPUT
- MD-{{slug}}-001: {{paste}}
- RP-{{slug}}-001 (RQ + H): {{paste}}
- Compute budget: {{...GPU·hr}}.

4. TASK
- Daftar dataset (versi, split, lisensi, ukuran) — termasuk subset bila pakai.
- Daftar baseline + cara reproduksi (commit hash / paper config).
- Define metric formally (rumus + library).
- Ablation matrix: variable × variant; sebut yang harus dilakukan vs nice-to-have.
- Seed policy: minimal 3 seed untuk hasil utama, 1 seed untuk ablation.
- Hyperparameter table dengan tuning protocol (mana di-tune, mana fixed, di mana di-tune (val), grid range).
- Compute budget breakdown.
- Fairness check: same compute, same data, same eval protocol.

5. OUTPUT
05-experiment-plan.md.

6. CONSTRAINTS
- **Tidak boleh tune di test.** Eksplisit pisahkan train/val/test.
- Setiap result number butuh ≥ 3 seed (untuk paper Q1).
- Setiap baseline butuh same data & same compute (atau dijelaskan).

7. ACCEPTANCE
- [ ] Dataset listed dengan versi.
- [ ] Baseline reproducible.
- [ ] Metric definisi formal.
- [ ] Ablation matrix.
- [ ] Compute budget realistic.
```

---

## Artifact Template — `EP-<paper-slug>-001`

```markdown
# Experiment Plan — {{Working Title}}

| Field | Value |
|---|---|
| ID | EP-{{slug}}-001 |
| Status | DRAFT |
| Linked MD | MD-{{slug}}-001 |

## 1. Datasets
| Dataset | Version | Split (train/val/test) | Size | License | Note |
|---|---|---|---|---|---|
| The Pile | v1 | 825GB / 1M / 1M | huge | MIT | LM PPL |
| LRA | v1 commit 0e6c6 | per task | medium | Apache-2 | long-range |
| Multimodal-LongBench | v0.3 | 80/10/10 | 50k | CC-BY | core eval |

Lisensi & data card cek manual.

## 2. Metrics
| Metric | Definition | Library |
|---|---|---|
| Perplexity (PPL) | exp(mean NLL) | HF eval |
| Accuracy (LRA) | per-task acc, then macro | LRA repo |
| Latency | mean over 100 batches, batch=1, fp16 | torch.profiler |
| Throughput | tokens/sec, batch=8 | own script |
| GPU memory | peak alloc | torch.cuda.max_memory_allocated |

## 3. Baselines
| Baseline | Source | Reproduce mode |
|---|---|---|
| Transformer (full attn) | HF | re-train at same params |
| Transformer-XL | repo X commit Y | re-train |
| Mamba | repo Z commit W | re-train; cite |
| Performer | repo P | re-train |

Same data, same tokens-trained, same compute.

## 4. Ablation Matrix
| Variable | Values | Purpose | Priority |
|---|---|---|---|
| Layer ratio r | 2, 4, 8 | RQ1 | MUST |
| Sparse attn window W | 64, 128, 256 | RQ1 | MUST |
| Stride S | 256, 512, 1024 | RQ1 | SHOULD |
| Sequence length | 4k, 8k, 16k, 32k | RQ2 | MUST |
| Model size | 350M, 760M, 1.3B | RQ2 | SHOULD (compute permitting) |
| Gating type | learned, fixed | RQ1 | NICE |

## 5. Seeds Policy
- Headline result: **5 seeds**.
- Ablation grid: **3 seeds**.
- Diagnostic probes: **3 seeds**.
- Mean ± std reported. Significance: paired t-test bila banding.

## 6. Hyperparameters
| HP | Value | Tuned? | Range |
|---|---|---|---|
| LR | 3e-4 | Yes (val) | 1e-4..1e-3 logspace 5 |
| Batch | 256 | Fixed | — |
| Steps | 200k | Fixed | — |
| Warmup | 4k | Fixed | — |
| Weight decay | 0.1 | Fixed | — |
| Dropout | 0.1 | Yes | 0.0..0.2 |

Tuning **only on val**. Test never seen.

## 7. Compute Budget
| Item | Cost |
|---|---|
| Headline (5 seeds × 4 model variants × 3 sizes) | ~1500 A100·hr |
| Ablation (3 seeds × 18 cells) | ~700 A100·hr |
| Probes | ~200 A100·hr |
| Buffer (debug + reruns) | ~600 A100·hr |
| **Total** | **~3000 A100·hr** |

## 8. Fairness
- All baselines trained with same: tokens, compute, val schedule.
- Same eval scripts (single repo).
- Same random seed for data shuffle (per seed-run).

## 9. Logging
- Track: wandb / mlflow.
- Save: train loss every 100 steps, val every 1k, checkpoint every 5k.
- Hardware: log GPU type, driver, framework version.

## 10. Reproducibility Artifacts (planned)
- Code: GitHub repo + frozen commit per result.
- Configs: per-experiment YAML.
- Seeds: documented.
- Eval scripts: separate repo dependencies.
- Datasets: scripts to download + checksum.
```
