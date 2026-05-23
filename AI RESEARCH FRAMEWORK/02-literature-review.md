# Stage 02 — Literature Review → Lit Review

**Code:** `LR` | **Output:** `LR-<paper-slug>-001`

## Purpose
Membaca, mengkategorikan, dan mengkritik state-of-the-art untuk **menemukan gap yang nyata**. Output Lit Review adalah input langsung untuk Related Work di paper Anda.

## DoR
- [ ] Domain Map siap dengan ≥ 10 anchor paper.

## DoD
- [ ] Lit Review memuat: ≥ 30 paper dengan ringkasan ≤ 5 baris masing-masing, taxonomy hubungan, perbandingan tabel (method × dataset × metric), gap statement (3–5 gap konkret).
- [ ] Setiap paper Anda **baca abstract minimal**, anchor papers Anda baca penuh.
- [ ] Tidak ada citation halusinasi.

---

## Prompt Template

```
1. ROLE
You are a meticulous literature surveyor. You categorize, compare, and critique without padding.

2. CONTEXT
Saya akan menulis paper Q1 di area {{topic}}. Saya perlu Lit Review untuk:
1. Memetakan SOTA.
2. Menemukan gap.
3. Justifikasi novelty saya.

3. INPUT
- DM-{{slug}}-001: {{paste taxonomy + anchor papers}}.
- 30 paper yang sudah saya kumpulkan (judul + abstract):
{{paste atau bibtex}}

4. TASK
- Kategorikan ke taxonomy (rujuk DM).
- Untuk tiap paper: 1 paragraf ringkasan (problem, method, key result, limitation).
- Tabel comparative: methods × datasets × headline metric.
- Identifikasi 3–5 gap **konkret** (bukan "more research is needed").
- Identifikasi cluster paper yang berlawanan / kontroversi.
- Sarankan 5 paper "harus dibaca lebih dalam" sebelum lanjut.

5. OUTPUT
02-lit-review.md.

6. CONSTRAINTS
- **TIDAK** boleh menambah citation yang tidak ada di INPUT.
- Setiap claim "no one has done X" harus berhati-hati: cek lagi (Anda mungkin miss paper).
- Gap statement harus actionable (bisa di-attack di paper Anda).

7. ACCEPTANCE
- [ ] 30+ paper terkategorisasi.
- [ ] Tabel comparative diisi.
- [ ] 3+ gap konkret.
- [ ] Tiap gap punya argumen "kenapa belum dipecahkan".
```

---

## Artifact Template — `LR-<paper-slug>-001`

```markdown
# Lit Review — {{Topic}}

| Field | Value |
|---|---|
| ID | LR-{{slug}}-001 |
| Status | DRAFT |
| Linked DM | DM-{{slug}}-001 |
| Paper count | 30+ |

## 1. Reading Method
- Skim: title + abstract + figures + conclusion (all 30+).
- Deep: full read, take notes (anchor papers, ~10).
- BibTeX collected in `papers.bib`.

## 2. Categorized Survey

### 2.1 Sparse Attention
| Paper | Year | Key Idea | Limitation |
|---|---|---|---|
| Longformer (Beltagy et al.) | 2020 | local + global tokens | task-specific global pattern |
| BigBird (Zaheer et al.) | 2020 | random + local + global | hard to scale beyond 4k |

### 2.2 Linear Attention
| Paper | Year | Key Idea | Limitation |
|---|---|---|---|
| Performer (Choromanski et al.) | 2021 | random feature kernel | accuracy gap on complex tasks |
| ... | | | |

### 2.3 State-Space Models
| Paper | Year | Key Idea | Limitation |
|---|---|---|---|
| S4 (Gu et al.) | 2022 | structured SSM | training instability early |
| Mamba (Gu, Dao) | 2024 | selective SSM | benchmarks limited initially |

## 3. Comparative Table (headline)

| Method | Year | LM PPL ↓ | LRA avg ↑ | Train compute | Long-seq capable |
|---|---|---|---|---|---|
| Transformer | 2017 | 18.3 | 53.0 | O(N²) | no (O(N²)) |
| Longformer | 2020 | 18.7 | 56.4 | O(N) local | yes (4k) |
| Performer | 2021 | 19.1 | 51.4 | O(N) | yes |
| Mamba | 2024 | 17.5 | 60.1 | O(N) | yes (1M+) |

## 4. Identified Gaps

### Gap 1 — Hybrid attention+SSM not systematically benchmarked on multimodal long context
- Why open: most SSM papers benchmark text/audio; multimodal under-explored.
- Why hard: dataset not standardized; eval metric ambiguous.
- Attackable? YES — contribute a benchmark + a baseline hybrid model.

### Gap 2 — {{...}}

### Gap 3 — {{...}}

## 5. Controversy / Open Debate
- Is selectivity (Mamba) vs full attention truly better, or just better at certain tasks?
- {{...}}.

## 6. Must-Re-read (for stage 03 proposal)
1. {{paper}} — ada potential overlap dengan ide saya.
2. {{paper}} — punya ablation yang akan saya kontraskan.
3. ...

## 7. Citation Hygiene
- All entries in `papers.bib` verified via Google Scholar / arXiv: ✅.
- Removed 2 hallucinated entries: {{...}}.
```
