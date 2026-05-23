# Stage 01 — Domain Scan → Domain Map

**Code:** `DS` | **Output:** `DM-<paper-slug>-001`

## Purpose
Memetakan "lay of the land" sebelum nyemplung. Apa subfield-subfield yang ada, siapa pemainnya, di mana boundary-nya, venue mana yang relevan.

## DoR
- [ ] Anda punya minat / keingintahuan kasar (1–2 kalimat).

## DoD
- [ ] Domain Map memuat: subfield taxonomy, top venues + impact, top labs/researchers, hot themes 2–3 tahun terakhir, identified blind spots.
- [ ] Daftar 10–20 paper anchor (yang Anda akan baca penuh di stage 02).

---

## Prompt Template

```
1. ROLE
You are a senior researcher who does meta-reviews. You can map a field rapidly without hallucinating citations.

2. CONTEXT
Saya tertarik di area: {{misal: efficient attention for long sequences}}.
Background saya: {{level PhD/master/undergrad/industri, bidang yang familiar}}.
Goal: paper Q1 dalam {{12 bulan}}.

3. INPUT
- Minat kasar: {{1–2 kalimat}}.
- Apa yang sudah saya tahu: {{1 paragraf}}.
- Constraint: compute, data, waktu.

4. TASK
- Sketsa taxonomy subfield (tree atau bullet).
- Sebut 5–8 top venue (conf + journal) yang relevan dengan ranking-nya (CORE/Scimago/h5-index).
- Sebut 5–10 lab/researcher aktif di area ini (verify-able names).
- Identifikasi 3 hot themes terakhir 2–3 tahun.
- Identifikasi 2–3 "blind spot" / under-explored area.
- Sarankan 10–20 anchor paper untuk dibaca penuh (judul + author + venue + tahun, no DOI sangkaan).

5. OUTPUT
01-domain-map.md.

6. CONSTRAINTS
- **TIDAK** boleh memberi sitasi yang tidak Anda yakin valid. Tandai "[VERIFY]" untuk yang ragu.
- Anchor paper harus dari venue Q1 atau yang sangat berpengaruh.

7. ACCEPTANCE
- [ ] Taxonomy ≥ 3 level kedalaman.
- [ ] 5+ venue dengan ranking.
- [ ] 10+ anchor paper.
- [ ] 2+ blind spot.
- [ ] Setiap sitasi yang ragu ditandai [VERIFY] (lalu Anda cek manual!).
```

---

## Artifact Template — `DM-<paper-slug>-001`

```markdown
# Domain Map — {{Topic}}

| Field | Value |
|---|---|
| ID | DM-{{slug}}-001 |
| Status | DRAFT |
| Date | {{YYYY-MM-DD}} |

## 1. Topic Statement
{{Apa minat Anda dalam 2 kalimat. Specific, not "AI in healthcare".}}

## 2. Taxonomy
- Efficient long-sequence modeling
  - Sparse attention
    - Local windows
    - Block-sparse / strided
  - Approximated attention
    - Linear / Performer-style
    - Low-rank
  - State-space models
    - SSM (S4/Mamba)
    - RWKV
  - Memory-augmented
    - External memory
    - Retrieval

## 3. Top Venues
| Venue | Type | Rank | h5 / IF |
|---|---|---|---|
| NeurIPS | conference | A* (CORE) | h5 ≈ 380 |
| ICML | conference | A* | h5 ≈ 280 |
| ICLR | conference | A* | h5 ≈ 300 |
| ACL / EMNLP | NLP-specific | A* | h5 ≈ 200 |
| TPAMI | journal | Q1 | IF ≈ 23 |
| JMLR | journal | Q1 | IF ≈ 6 |
| TMLR | journal | open | rolling |

## 4. Active Researchers / Labs
| Researcher / Lab | Affiliation | Why relevant |
|---|---|---|
| {{...}} | {{...}} | {{...}} |

## 5. Hot Themes 2023–2025
- Mamba / SSM resurgence.
- Efficient inference for million-token contexts.
- Hybrid attention + recurrence.

## 6. Blind Spots / Under-explored
- {{...}} — argumen mengapa under-explored.
- {{...}}.

## 7. Anchor Papers (read fully)
| # | Title | Authors | Venue | Year | Verified? |
|---|---|---|---|---|---|
| 1 | Attention Is All You Need | Vaswani et al. | NeurIPS | 2017 | ✅ |
| 2 | Mamba: Linear-Time Sequence Modeling | Gu, Dao | preprint/ICLR | 2024 | ✅ |
| 3 | {{...}} | {{...}} | {{...}} | {{...}} | [VERIFY] |
| ... | | | | | |

## 8. Reading Plan
- Week 1: anchors 1–6 (foundational).
- Week 2: anchors 7–14 (recent SOTA).
- Week 3: anchors 15–20 (adjacent / contrarian).
```
