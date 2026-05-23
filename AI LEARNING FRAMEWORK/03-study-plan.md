# Stage 03 — Study Plan → Study Plan

**Code:** `SP` | **Output:** `SP-<topic-slug>-001`

## Purpose
Mengubah Topic Map jadi jadwal mingguan/harian yang realistis.

## DoD
- [ ] Study Plan: jadwal per minggu (subtopik + resource + outcome mingguan), milestone tiap 2–4 minggu, slot review.

## Prompt
```
ROLE: study planner yang realistis (bukan motivasi-poster).
INPUT: TM-{{slug}}-001 + jam tersedia/minggu + commitment lain.
TASK:
- Pecah jadi blok mingguan (minggu 1..N).
- Tiap minggu: 1–2 subtopik utama + outcome (apa yang bisa dilakukan akhir minggu).
- Slot review tiap minggu (Sabtu / akhir minggu).
- Milestone tiap 2–4 minggu (assessment kecil: quiz, mini project).
- Build buffer: 20% slack untuk hari sakit / off mood.
OUTPUT: 03-study-plan.md.
CONSTRAINTS: total jam plan ≤ 80% jam tersedia (anti burnout).
ACCEPTANCE: jadwal mingguan, outcome per minggu, milestone, slack tertulis.
```

## Template
```markdown
# Study Plan — {{Topic}}

| Field | Value |
|---|---|
| ID | SP-{{slug}}-001 |
| Linked TM | TM-{{slug}}-001 |
| Hours/week available | {{N}} |
| Hours/week planned | {{≤ 0.8 × N}} |

## Weekly Schedule

### Week 1 — Foundation/X
- **Subtopic:** {{...}}
- **Resource:** chapter 1–3 of {{Book}}.
- **Practice:** 5 small exercises end-of-chapter.
- **Outcome:** Saya bisa {{verb}} {{object}}.
- **Hours:** 7 of 9.

### Week 2 — Foundation/X cont.
- ...

### Week 3 — Foundation/Y
...

## Milestones
| Week | Milestone | Eval method |
|---|---|---|
| 4 | Mini Project A | Self-check: produces correct output for 5 test cases |
| 8 | Mini Project B | Pair-review with peer / mentor |
| 12 | Capstone start | — |
| 16 | Capstone done | Public release / demo |

## Buffer Days
- Skip 1 sesi/minggu jika perlu (sudah dihitung dalam 80% rule).
- 1 minggu buffer total dipasang di week 8 untuk konsolidasi.
```
