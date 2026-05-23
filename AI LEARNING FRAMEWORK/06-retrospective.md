# Stage 06 — Retrospective → Retrospective

**Code:** `RT` | **Output:** `RT-<topic-slug>-001`

## Purpose
Konsolidasi: apa yang stuck, apa yang nguap, apa yang berikutnya. Tanpa retrospektif, kesalahan yang sama akan terjadi di siklus belajar berikutnya.

## DoD
- [ ] Retrospective memuat: outcome vs goal, top 3 win, top 3 mistake, knowledge gap yang masih ada, next learning step, "do/don't" untuk siklus depan.

## Prompt
```
ROLE: coach pasca-pelatihan. Tugas: jujur tapi konstruktif.
INPUT: LG, SP plan vs realisasi, NL ringkas, CP outcome.
TASK:
- Compare actual outcome vs goal (% achieved).
- Identifikasi 3 win (apa yang bekerja).
- Identifikasi 3 mistake (apa yang salah/lambat).
- Knowledge yang masih lemah → rencana review.
- Sarankan next learning topic (deepen vs broaden).
OUTPUT: 06-retrospective.md.
CONSTRAINTS: jujur, hindari "I should have studied harder" tanpa root cause.
ACCEPTANCE: 3 win, 3 mistake, gap mapping, next step.
```

## Template
```markdown
# Retrospective — {{Topic}}

| Field | Value |
|---|---|
| ID | RT-{{slug}}-001 |
| Period | {{start..end}} |
| Linked LG | LG-{{slug}}-001 |

## 1. Goal vs Reality
| Goal element | Target | Actual | % |
|---|---|---|---|
| Outcome SMART | bisa X | mostly X (Z masih lemah) | 80% |
| Capstone | 1 project | 1 project (basic, not polished) | 70% |
| Hours | 9/wk | 6/wk avg | 67% |

## 2. Wins
- W1: {{spaced repetition Anki dipakai konsisten}}.
- W2: {{...}}.
- W3: {{...}}.

## 3. Mistakes & Root Cause
| # | What went wrong | Root cause | Lesson |
|---|---|---|---|
| 1 | Skip latihan minggu 3 | merasa "sudah ngerti" tapi belum | latihan tetap wajib, bukan opsional |
| 2 | Project terlalu ambisius | scope tidak dipotong | scope half-half |
| 3 | Tidak share publik | takut judgement | share even ugly |

## 4. Knowledge Gaps Remaining
- Subtopic X — paham konsep, belum praktik.
- Subtopic Y — paham basic, belum advance.

Rencana: review 30 menit/minggu selama 4 minggu.

## 5. Next Step
- **Deepen:** advance pada {{subtopic Y}} via {{resource}}.
- **Broaden:** topic lain yang adjacent: {{...}}.
- Pilih: {{...}}.

## 6. Do / Don't for Next Cycle
- DO: bikin recall test 1×/minggu.
- DO: pecah project lebih kecil.
- DON'T: skip latihan walau merasa "ngerti".
- DON'T: belajar > 2 topic paralel.
```
