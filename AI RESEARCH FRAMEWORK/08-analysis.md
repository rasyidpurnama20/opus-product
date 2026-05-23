# Stage 08 — Analysis → Analysis Report

**Code:** `AN` | **Output:** `AR-<paper-slug>-001`

## Purpose
Mengubah angka jadi **insight**. Apa yang berhasil, apa yang gagal, *kenapa*, dan apa batasnya. Stage ini adalah pondasi Section "Discussion" di paper Anda.

## DoR
- [ ] Results Pack siap (semua run selesai).

## DoD
- [ ] Analysis Report memuat: jawaban tegas tiap RQ (didukung angka), apakah hipotesis confirmed/refuted, mekanistik insight (kenapa method bekerja), threats to validity, limitations, scope of generalization.

---

## Prompt Template

```
1. ROLE
You are a senior researcher who interprets results without over-claiming.
You use phrases like "consistent with H1" not "proves H1".

2. CONTEXT
Saya butuh analisis hasil sebelum drafting paper.

3. INPUT
- RP-{{slug}}-001 (RQs + H): {{paste}}
- RPK-{{slug}}-001 (results): {{paste tabel headline + ablation}}.

4. TASK
- Untuk tiap RQ: jawaban tegas + bukti pendukung (tabel mana, angka mana).
- Untuk tiap H: confirmed / partially / refuted, dengan magnitude.
- Identifikasi 2–3 mekanistik insight (mengapa hybrid bekerja: gating? layer ratio? selectivity?). Bedakan claim vs spekulasi.
- Threats to validity:
  - Internal: hyperparameter tuning, seed variance, leakage.
  - External: dataset bias, domain coverage.
  - Construct: apakah metric mengukur yang Anda klaim?
- Limitations: jujur (bukan boilerplate).
- Scope: hasil ini valid dalam kondisi apa?

5. OUTPUT
08-analysis.md.

6. CONSTRAINTS
- Hindari over-claim ("proves", "shows definitively").
- Setiap claim punya angka pendukung (tabel/figure ref).
- Limitations ≥ 3, jujur.

7. ACCEPTANCE
- [ ] Tiap RQ dijawab dengan bukti.
- [ ] Tiap H di-evaluasi.
- [ ] Threats to validity 3 kategori.
- [ ] Limitations konkret (≥ 3).
```

---

## Artifact Template — `AR-<paper-slug>-001`

```markdown
# Analysis Report — {{Working Title}}

| Field | Value |
|---|---|
| ID | AR-{{slug}}-001 |
| Status | DRAFT |
| Linked RPK | RPK-{{slug}}-001 |

## 1. RQ Verdicts

### RQ1: Bisakah hybrid match full-attention quality?
- **Verdict:** YA, dalam scope yang diuji.
- **Evidence:** Tabel 1 — Hybrid 60.6 ± 0.2 vs Mamba 60.1 ± 0.3 vs Transformer 53.4 ± 0.5 di LRA. p<0.05 vs Mamba.
- **Caveat:** Hanya untuk seq ≤ 32k; > 32k tidak diuji.

### RQ2: Trade-off accuracy vs latency?
- **Verdict:** Hybrid Pareto-dominate Transformer untuk seq ≥ 8k.
- **Evidence:** Fig 2 — accuracy maintain, latency 2.3× lebih rendah pada seq=16k.

### RQ3: Failure mode hybrid?
- **Verdict:** Konsisten gagal pada exact retrieval task; kompetitif lain.
- **Evidence:** Tabel 4 — pada Needle-in-Haystack acc 78% vs Transformer 92%.

## 2. Hypothesis Verdicts
| H | Predicted | Observed | Verdict |
|---|---|---|---|
| H1 (PPL diff ≤ 0.3) | Δ ≤ 0.3 | Δ = 0.1 | confirmed |
| H2 (throughput ≥ 2× at 16k) | ≥ 2× | 2.3× | confirmed |
| H3 (failure on retrieval) | yes | yes | confirmed |

## 3. Mechanistic Insights
- **Insight 1 — Selectivity is the workhorse, not attention.** Ablation A1 menunjukkan menaikkan attention layer dari 1/4 ke 1/2 hampir tidak menaikkan acc. Selectivity gating SSM yang mendorong long-range mixing.
- **Insight 2 — Sparse window cukup untuk konteks lokal.** Stride global tokens menambah accuracy hanya pada task multi-hop (Tabel 5). Pada task lain, window saja sudah cukup.
- **Insight 3 — (Speculative) Hybrid mungkin lebih robust ke domain shift.** Kami lihat trend kecil di {{...}} tapi belum signifikan; flagged for future work.

## 4. Threats to Validity

### Internal
- Hyperparameter di-tune untuk Hybrid; baseline Performer pakai HP dari paper aslinya. Mitigasi: kami juga tune Performer dengan budget yang sama (Tabel S3).
- Mixed precision (fp16) bisa menyebabkan small variance; semua model pakai sama.

### External
- Dataset multimodal kami terbatas pada gambar+teks; audio belum.
- Bahasa: dominan Inggris. Generalisasi ke bahasa lain belum diuji.

### Construct
- Latency diukur pada batch=1 fp16. Hasil bisa berbeda untuk produksi batched/quantized.
- LRA sebagai proxy long-range mungkin tidak menangkap semua aspek "long context".

## 5. Limitations
- Skalanya max 1.3B; perilaku pada 7B+ belum diuji.
- Kami tidak melatih dari skratch pada multimodal-LongBench (compute), pakai fine-tune.
- Failure mode pada retrieval belum diperbaiki — flagged for follow-up.

## 6. Scope of Generalization
Hasil paper ini kuat untuk: text + image, seq 4k–32k, model 350M–1.3B, English-dominant. Hasil **tidak** mengklaim generalisasi ke: audio, RL, ≥ 7B, languages selain English, real-time inference.
```
