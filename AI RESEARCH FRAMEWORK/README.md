# AI RESEARCH FRAMEWORK

Framework prompt untuk **riset akademik AI/ML** dengan target publikasi di venue **Q1** (mis. NeurIPS, ICML, ICLR, CVPR, ACL, EMNLP, AAAI, IEEE TPAMI, JMLR, Nature MI, dst — atau jurnal Q1 di Scimago/JCR untuk bidang spesifik Anda).

Framework ini menekankan **rigor**, **reproducibility**, dan **anti-halusinasi** — karena AI sangat mudah mengarang sitasi, salah quote angka, atau membuat klaim novelty yang sebenarnya sudah ada.

## Prinsip
1. **Verify, don't trust.** Setiap sitasi yang AI sarankan **wajib** Anda cek manual di Google Scholar / arXiv / venue resmi. AI sering halusinasi judul, author, tahun.
2. **Novelty is earned, not claimed.** Hanya klaim "novel" setelah literature review tuntas.
3. **Ablations > main results.** Reviewer Q1 lebih percaya ablation yang menjelaskan *mengapa* daripada SOTA single-number.
4. **Reproducibility from day 1.** Seed, env, data version, code repo dicatat sejak run pertama.
5. **Write to the reviewer in your head.** Setiap stage tanya: "kalau saya reviewer, apa yang akan saya tolak?"
6. **Statistical honesty.** Mean ± std minimal 3 seeds untuk hasil utama; significance test bila banding.

## Stages

```
[01-Domain Scan]    ──► Domain Map (DM)            ← lay of the land
       │
       ▼
[02-Literature]     ──► Lit Review (LR)            ← taxonomy + gaps
       │
       ▼
[03-Proposal]       ──► Research Proposal (RP)     ← RQ + hypothesis + claims
       │
       ▼
[04-Method]         ──► Method Design (MD)         ← what to build/measure
       │
       ▼
[05-Experiment]     ──► Experiment Plan (EP)       ← protocol, ablations, budget
       │
       ▼
[06-Implementation] ──► Reproducible Codebase (RC)
       │
       ▼
[07-Results]        ──► Results Pack (RPK)         ← raw numbers + figures
       │
       ▼
[08-Analysis]       ──► Analysis Report (AR)       ← interpretation, threats
       │
       ▼
[09-Drafting]       ──► Draft Paper (DP)           ← per-section draft
       │
       ▼
[10-Submission]     ──► Submission Pack (SUB)      ← cover, supp, checklist
       │
       ▼
[11-Rebuttal]       ──► Rebuttal Plan (RBP)        ← response strategy
```

| # | Stage | Output | Code |
|---|---|---|---|
| 01 | Domain Scan | Domain Map | `DM` |
| 02 | Literature Review | Lit Review | `LR` |
| 03 | Proposal | Research Proposal | `RP` |
| 04 | Method Design | Method Design | `MD` |
| 05 | Experiment Plan | Experiment Plan | `EP` |
| 06 | Implementation | Reproducible Codebase | `RC` |
| 07 | Results | Results Pack | `RPK` |
| 08 | Analysis | Analysis Report | `AR` |
| 09 | Drafting | Draft Paper | `DP` |
| 10 | Submission | Submission Pack | `SUB` |
| 11 | Rebuttal | Rebuttal Plan | `RBP` |

## Konvensi ID
`<CODE>-<paper-slug>-<NNN>`. Contoh `LR-attention-survey-001`, `EP-attention-001`.

## Folder Layout
```
research/<paper-slug>/
├── 01-domain-map.md
├── 02-lit-review.md
├── 03-proposal.md
├── 04-method.md
├── 05-experiment-plan.md
├── 06-codebase/         ← link / submodule
├── 07-results/          ← csv, json, plots
├── 08-analysis.md
├── 09-paper/            ← LaTeX project
├── 10-submission/       ← cover letter, supp, checklist
└── 11-rebuttal.md
```

## AI-Specific Anti-Pattern
- Membiarkan AI menulis "according to (Smith et al., 2023)" tanpa verify — hampir pasti hallucinated.
- Hanya melaporkan single seed.
- Pilih baseline yang sengaja lemah.
- Klaim "first to do X" tanpa search ekstensif.
- Test set bocor ke training (data leakage).
- Hyperparameter tuning di test set.
