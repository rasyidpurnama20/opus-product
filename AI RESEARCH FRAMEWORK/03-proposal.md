# Stage 03 — Proposal → Research Proposal

**Code:** `PR` | **Output:** `RP-<paper-slug>-001`

## Purpose
Mengkristalkan **research question (RQ)**, **hipotesis**, dan **klaim kontribusi** sebelum mendesain method. Tanpa stage ini, Anda akan terjebak "tweak hyperparameter" tanpa narasi.

## DoR
- [ ] Lit Review siap dengan gap statements.

## DoD
- [ ] Research Proposal memuat: 1 RQ utama (+ 2–3 sub-RQ), hipotesis (yang bisa di-falsify), claims kontribusi (≤ 3, eksplisit), novelty argument vs related work, evaluation plan kasar, scope.
- [ ] Approve oleh diri sendiri (atau supervisor) sebelum lanjut ke method.

---

## Prompt Template

```
1. ROLE
You are a senior research advisor. You sharpen vague ideas into testable hypotheses.

2. CONTEXT
Saya menyiapkan paper Q1 berdasarkan gap di Lit Review.

3. INPUT
- LR-{{slug}}-001 gaps:
{{paste gap section}}
- Resource saya: compute {{...}}, data access {{...}}, waktu {{...}}.

4. TASK
- Reformulasikan gap pilihan jadi 1 RQ utama yang clear, narrow, testable.
- Pecah jadi 2–3 sub-RQ.
- Tulis hipotesis (H1, H2, ...) yang bisa di-falsify, lengkap dengan prediksi numerik kalau bisa.
- Tulis 2–3 kontribusi: setiap kontribusi punya format "we propose X, which enables Y, demonstrated by Z".
- Argumenkan novelty: untuk tiap claim, sebut paper terdekat dan apa yang berbeda.
- Evaluation plan: dataset, metric, baseline minimum.
- Scope: in/out of scope.
- Risiko: kalau hipotesis salah, apa rencana kontingensi?

5. OUTPUT
03-proposal.md.

6. CONSTRAINTS
- RQ tidak boleh "is X better than Y" tanpa kondisi spesifik.
- Hipotesis harus falsifiable.
- Klaim novelty harus disertai paper pembanding eksplisit.

7. ACCEPTANCE
- [ ] RQ + sub-RQ jelas.
- [ ] Hipotesis falsifiable + (idealnya) numerik.
- [ ] ≤ 3 kontribusi.
- [ ] Setiap claim novelty dipasangkan ke paper terkait.
- [ ] Risiko + plan B ada.
```

---

## Artifact Template — `RP-<paper-slug>-001`

```markdown
# Research Proposal — {{Working Title}}

| Field | Value |
|---|---|
| ID | RP-{{slug}}-001 |
| Status | DRAFT |
| Linked LR | LR-{{slug}}-001 |
| Target venue | {{NeurIPS / ICML / ICLR / TPAMI / ...}} |
| Target submission | {{deadline date}} |

## 1. Research Question
**RQ:** Can a hybrid attention + selective SSM model match full-attention quality on long-context multimodal tasks while preserving O(N) inference?

### Sub-RQs
- **RQ1:** Apakah selective gating SSM cukup untuk menggantikan global attention di setting multimodal?
- **RQ2:** Bagaimana trade-off accuracy vs latency vs memory antara hybrid vs full attention vs full SSM?
- **RQ3:** Apa pola failure ketika hybrid gagal?

## 2. Hypotheses
- **H1:** Hybrid (attention every 4 layers + SSM rest) mencapai PPL ≤ full-attention baseline (∆ ≤ 0.3) pada multimodal long-context benchmark.
- **H2:** Hybrid menunjukkan inference latency O(N) untuk N ≥ 8k, dengan throughput ≥ 2× full-attention pada N = 16k.
- **H3:** Failure mode hybrid dominan di task yang membutuhkan exact in-context retrieval (we expect this; will quantify).

## 3. Contributions (≤ 3)
- **C1:** Sebuah arsitektur Hybrid-AS yang menggabungkan attention sparse + selective SSM dengan skema layer-interleave terbukti optimal lewat ablation.
- **C2:** Evaluasi sistematis pada {{benchmark}} dengan {{N}} ablation, menetapkan trade-off accuracy/efficiency curve.
- **C3:** Analisis failure mode dengan 3 diagnostic probe baru (retrieval, length-extrapolation, modality-bias).

## 4. Novelty Argument
| Claim | Closest prior work | Difference |
|---|---|---|
| C1 (hybrid AS) | {{Paper X (2024)}} | mereka attention+RNN, kami attention+selective SSM, berbeda gating |
| C2 (benchmark eval) | {{Paper Y}} | mereka unimodal; kami multimodal |
| C3 (failure mode probe) | {{none directly}} | new diagnostic probes |

## 5. Evaluation Plan (rough)
- **Datasets:** {{LRA, ImageNet long-form, Multimodal-LongBench}}.
- **Baselines:** Transformer-XL, Mamba, Performer, full-attention Transformer.
- **Metrics:** PPL / accuracy + latency + GPU memory + throughput.
- **Ablations:** layer-interleave ratio (1/2/4/8), gating mechanism, sequence length.

## 6. Scope
- **In:** model size ≤ 1.3B, sequence length ≤ 32k.
- **Out:** scaling laws beyond 1.3B (separate work).

## 7. Risks & Plan B
| Risk | Likelihood | Plan B |
|---|---|---|
| Hybrid tidak match full-attention | Med | reframe paper as "trade-off study" rather than "match"; still publishable |
| Compute insufficient for ≥ 1B | Med | run scale at 350M, extrapolate, mention as limitation |
| Benchmark Multimodal-LongBench tidak stabil | Low | switch to {{alternatif}} |

## 8. Timeline (rough)
| Month | Milestone |
|---|---|
| 1 | Codebase + baseline reproduce |
| 2 | Hybrid implementation + small-scale ablation |
| 3 | Full ablation suite |
| 4 | Failure mode probes + analysis |
| 5 | Drafting |
| 6 | Internal review + submit |

## 9. Approval
- [ ] Self-review.
- [ ] Supervisor sign-off (date / name).
```
