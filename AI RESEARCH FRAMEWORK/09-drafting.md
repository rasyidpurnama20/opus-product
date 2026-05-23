# Stage 09 — Drafting → Draft Paper

**Code:** `DR` | **Output:** `DP-<paper-slug>-001` (LaTeX project)

## Purpose
Menulis draft paper section-by-section dengan disiplin yang benar: bukan dump informasi, tapi narasi yang menjawab "kenapa peduli, kenapa percaya, apa konsekuensi".

## DoR
- [ ] Analysis Report `APPROVED`.

## DoD
- [ ] Draft lengkap (Abstract, Intro, Related Work, Method, Experiments, Results, Discussion, Conclusion, References).
- [ ] Limitations section eksplisit.
- [ ] Ethics / impact statement (bila venue minta).
- [ ] Reproducibility statement.
- [ ] Tabel & figure final caption.
- [ ] Pass internal review minimal 1 kolega.

---

## Prompt Template (per section, jangan satu prompt untuk seluruh paper)

```
1. ROLE
You are a senior author at a Q1 venue. You write tight, precise paragraphs.

2. CONTEXT
Saya menyusun Section {{X}} dari paper.

3. INPUT
- Section yang ingin ditulis: {{Abstract / Introduction / Related Work / Method / ...}}
- Sumber materi:
  - RP-{{slug}}-001 (RQ + claims)
  - MD-{{slug}}-001 (method)
  - EP-{{slug}}-001 (experiments)
  - RPK-{{slug}}-001 (results)
  - AR-{{slug}}-001 (analysis)
  - {{paste relevant section}}

4. TASK
Tulis draft Section {{X}} mengikuti panduan venue:
- {{count}} kata target.
- Struktur paragraf yang dianjurkan untuk section ini (lihat panduan section di bawah).

5. OUTPUT
Section LaTeX (.tex), simpan sebagai `paper/sections/{{x}}.tex`.

6. CONSTRAINTS
- Hindari hype words (groundbreaking, revolutionary, novel-novel-novel).
- Setiap claim ada bukti (tabel/figure ref atau citation).
- Pakai notasi yang konsisten dengan MD.
- **TIDAK** memasukkan citation yang belum diverifikasi.

7. ACCEPTANCE
- [ ] Memenuhi struktur section.
- [ ] Setiap claim punya backing.
- [ ] Tidak ada placeholder \cite{TODO}.
```

---

## Section-by-Section Guide

### Abstract (≤ 200 kata)
Struktur: 1 kalimat motivasi → 1 kalimat gap → 1 kalimat kontribusi (kami propose X) → 1–2 kalimat metode singkat → 1 kalimat hasil utama (angka konkret) → 1 kalimat dampak / outlook.

### Introduction (~1 halaman)
- Paragraf 1: motivasi luas, pertanyaan besar.
- Paragraf 2: status quo & gap (rujuk paper besar 2–3, jangan banjir sitasi).
- Paragraf 3: ide kunci kami dalam 1 kalimat + figure 1 (overview).
- Paragraf 4: ringkasan kontribusi (bullet 3 buah).
- Paragraf 5: outline paper.

### Related Work (~½ halaman)
- Cluster, bukan listing kronologis. 3–4 cluster, 1 paragraf masing-masing.
- Bandingkan posisi paper Anda dengan tiap cluster.

### Method (Section 3, 2–3 halaman)
- Notasi tabel di awal.
- Diagram arsitektur (Figure 2).
- Sub-section per komponen baru.
- Pseudo-code untuk komponen kritis.
- Complexity analysis (table).

### Experiments (Section 4, 3–4 halaman)
- 4.1 Setup: dataset, baseline, metric, training.
- 4.2 Headline result.
- 4.3 Ablation studies (per RQ).
- 4.4 Diagnostic / failure mode.
- 4.5 Efficiency analysis.

### Discussion (½–1 halaman)
- Implication terbesar.
- Connection ke RQ.
- Limitations (eksplisit, ≥ 3 paragraf bullet).
- Future work konkret.

### Conclusion (≤ ½ halaman)
- Re-state kontribusi singkat.
- 1 paragraf "broader implication" tanpa over-claim.

### References
- Bibtex bersih, sortir alfabetik / by venue per house style.
- Tidak ada arXiv-only kalau versi published tersedia.

---

## Artifact Template — `DP-<paper-slug>-001`

```markdown
# Draft Paper — {{Working Title}}

| Field | Value |
|---|---|
| ID | DP-{{slug}}-001 |
| Status | DRAFT v0.5 |
| Linked AR | AR-{{slug}}-001 |
| Target venue | {{...}} |
| Word count | {{...}} / target {{...}} |

## Layout
```
paper/
├── main.tex
├── sections/
│   ├── 00_abstract.tex
│   ├── 01_introduction.tex
│   ├── 02_related.tex
│   ├── 03_method.tex
│   ├── 04_experiments.tex
│   ├── 05_discussion.tex
│   ├── 06_conclusion.tex
│   ├── 07_limitations.tex
│   ├── 08_ethics.tex
│   └── 09_repro.tex
├── figures/
├── tables/
└── references.bib
```

## Internal Review Pass
- [ ] Reviewer 1 (kolega): {{nama}}, date, comments resolved.
- [ ] Reviewer 2: {{...}}.
- [ ] Final read-through aloud.

## Pre-Submit Checklist
- [ ] All `\cite{TODO}` resolved.
- [ ] Figure resolution ≥ 300 dpi.
- [ ] Tables fit page; horizontal lines minimal (booktabs).
- [ ] Notation consistent throughout.
- [ ] Limitations dipakai jujur (≥ 3 bullet).
- [ ] Ethics statement (kalau venue mensyaratkan).
- [ ] Reproducibility statement (link repo + commit).
- [ ] Author affiliation, funding ack lengkap.
```
