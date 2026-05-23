# Stage 11 — Rebuttal → Rebuttal Plan

**Code:** `RB` | **Output:** `RBP-<paper-slug>-001`

## Purpose
Menanggapi review dengan strategi: yang penting dijawab dulu, dukung dengan data, jangan defensif. Rebuttal yang kuat sering mengubah skor 4→6 atau 5→7.

## DoR
- [ ] Reviews keluar.

## DoD
- [ ] Rebuttal Plan memuat: triage komen per reviewer (positive / valid concern / misunderstanding / out of scope), prioritized action plan dalam batas waktu rebuttal, draft response per concern.
- [ ] Submit rebuttal sebelum deadline.

---

## Prompt Template

```
1. ROLE
You are a senior author handling a rebuttal under time pressure.
You answer concerns with evidence, not rhetoric.

2. CONTEXT
Saya dapat {{N}} review. Score: {{...}}. Deadline rebuttal: {{...}}.

3. INPUT
- Review verbatim per reviewer:
{{paste R1, R2, R3, ...}}
- AC summary:
{{paste, kalau ada}}
- Tabel results & ablation: {{ringkas}}.

4. TASK
- Triase per komen: A=critical-flaw, B=valid-but-fixable, C=misunderstanding, D=out-of-scope-future.
- Estimasi waktu untuk fix tiap A/B (run extra ablation? new figure? rewrite sub-section?).
- Prioritaskan: yang menggerakkan score paling banyak.
- Draft response per concern (kalimat netral, gunakan "we appreciate" sparingly, fokus bukti).
- Identifikasi extra experiment yang feasible dalam jendela rebuttal.
- Sketsa global response (untuk semua reviewer): 1 paragraf naratif.

5. OUTPUT
11-rebuttal-plan.md.

6. CONSTRAINTS
- Tidak menyerang reviewer.
- Tidak janjikan eksperimen yang tidak akan sempat dijalankan.
- Setiap response: claim → bukti.
- Hormati word/character limit per response (venue specific).

7. ACCEPTANCE
- [ ] Triase per komen.
- [ ] Action plan dengan estimasi waktu.
- [ ] Draft response per komen kritis.
- [ ] Global response.
```

---

## Artifact Template — `RBP-<paper-slug>-001`

```markdown
# Rebuttal Plan — {{Working Title}}

| Field | Value |
|---|---|
| ID | RBP-{{slug}}-001 |
| Venue | {{...}} |
| Deadline | {{...}} |
| Initial scores | R1:5  R2:4  R3:6  R4:5 |
| Target scores | R1:6  R2:5+  R3:7  R4:6 |

## 1. Triage Matrix
| ID | Reviewer | Concern (1 line) | Class | Priority | Estimated Effort |
|---|---|---|---|---|---|
| C-01 | R2 | "ablation tidak cover gating type" | B (fixable) | HIGH | 1 day run, 1 day write |
| C-02 | R1 | "method derivation ambiguous in eq 4" | C (misunderstanding) | HIGH | 30 min clarify |
| C-03 | R3 | "novelty unclear vs Hybrid-X" | C (need explicit comparison) | HIGH | 2 hours diff table |
| C-04 | R4 | "missing failure case" | B | MED | already in supp; pointer |
| C-05 | R2 | "must run on 7B" | A-but-out-of-scope | LOW | not feasible in rebuttal |
| C-06 | R1 | "minor typo p.4" | C | LOW | trivial |

## 2. Action Plan (within rebuttal window)
| Action | Owner | Day |
|---|---|---|
| Run gating ablation (3 seeds) | me | D1–D2 |
| Add diff-vs-Hybrid-X table | me | D2 |
| Write response paragraph per concern | me | D3 |
| Co-author review responses | coauthor | D4 |
| Submit | me | D5 morning |

## 3. Draft Responses

### Response to R2 — Concern C-01 (gating ablation)
> We appreciate this suggestion. Following the reviewer, we ran an ablation comparing learned vs fixed gating across three seeds. Results (added in revised Table 6): learned gating 60.6 ± 0.2, fixed gating 58.9 ± 0.3 on LRA. The ~1.7 point gap supports our design choice. Code/log added to anon repo, commit `xxxxx`.

### Response to R1 — Concern C-02 (eq 4 ambiguity)
> Eq 4 defines $h_t$ as the hidden state at step t (not layer l). To remove ambiguity, in the revised version we (i) split into two equations (forward at step t, then layer l), (ii) clarify in caption, (iii) add a worked example in App A. The mathematical claim is unchanged.

### Response to R3 — Concern C-03 (novelty vs Hybrid-X)
> Hybrid-X (Smith et al. 2024) combines attention with RNN, not selective SSM. The selectivity gating is the key difference: it allows input-dependent state update (cf. Mamba), whereas RNN in Hybrid-X has fixed dynamics. We add a side-by-side comparison table to Section 2 (Table 2) and re-run our model with their layer ratio for direct comparison (60.6 vs 58.1 on LRA, see new Table 7).

### Response to R4 — Concern C-04 (missing failure)
> Failure case analysis is in Appendix C (currently 4 pages). We highlight in revised Section 4.4 with cross-ref to App C. Specifically, hybrid drops 14 acc points on Needle-in-Haystack vs Transformer; we discuss probable cause (lack of exact retrieval pathway) and propose mitigation (sec C.3).

### Response to R2 — Concern C-05 (7B scale)
> We agree that 7B+ scale is an important next step. Within the rebuttal window we cannot run training at this scale (cost ~100k GPU-hr). We discuss this limitation in Section 5 and outline a path forward (LR schedule extrapolation per Hoffmann et al.). We will pursue this in follow-up work.

## 4. Global Response (1 paragraf di atas semua individual)
> We thank reviewers for the thorough engagement. The most actionable concerns are addressed with new experiments (gating ablation, Hybrid-X comparison) and clarifications (eq 4, novelty positioning). Our headline claims remain unchanged: hybrid attention + selective SSM matches full-attention quality at O(N) inference for sequence lengths up to 32k and model sizes up to 1.3B; failure modes are explicit and discussed. Below we respond to each reviewer in detail. All revisions visible in the diff PDF and in the anonymized repo at commit `xxxxx`.

## 5. Risk
- C-05 might still keep R2 dissatisfied. Strategy: be honest about scope; emphasize the 1.3B result is already 4× larger than most ablation studies in the area.

## 6. Post-Rebuttal Plan
- Track AC-suggested revisions for camera-ready.
- Update repo with revised version on acceptance.
- Lessons-learned doc for next paper.
```
