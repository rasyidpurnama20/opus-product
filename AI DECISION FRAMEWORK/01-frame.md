# Stage 01 — Frame → Decision Brief

**Code:** `FR` | **Output:** `DB-<decision-slug>-001`

## Purpose
Tentukan keputusan apa yang sebenarnya harus diambil dan urgensinya, sebelum menggali opsi.

## DoD
- [ ] DB memuat: decision question (1 kalimat), context, deadline, reversibility (low/med/high), stakeholders, success-vs-failure look-like.

## Prompt
```
ROLE: framing coach, mempertanyakan asumsi keputusan.
INPUT: situasi mentah dari saya.
TASK:
- Reformulasikan jadi decision question 1 kalimat (mulai dengan "Should we / Apakah kita...").
- Cek: ini decision atau dilemma? Apakah ini sebenarnya 2 keputusan terpisah?
- Reversibility: apakah bisa di-undo dalam 1 minggu / 1 bulan / tidak bisa?
- Deadline: kapan harus diputuskan? Apa konsekuensi telat?
- Stakeholders: siapa terdampak.
- "Success looks like" + "Failure looks like" dalam 6 bulan.
OUTPUT: 01-decision-brief.md.
CONSTRAINTS: tidak menyarankan opsi di stage ini.
ACCEPTANCE: question, reversibility, deadline, stakeholders.
```

## Template
```markdown
# Decision Brief — {{title}}

| Field | Value |
|---|---|
| ID | DB-{{slug}}-001 |
| Status | DRAFT |
| Date | {{...}} |

## 1. Decision Question
> {{1 kalimat: "Should we adopt Postgres or stay with MongoDB for the analytics service?"}}

## 2. Context
{{Latar belakang: situasi sekarang, apa yang memicu pertanyaan, kenapa sekarang.}}

## 3. Reversibility
- Level: low / **medium** / high.
- If we go and want to revert: cost ≈ {{...}}, time ≈ {{...}}.

## 4. Deadline
- Decision by: {{date}}.
- Consequence of delay: {{...}}.

## 5. Stakeholders
| Stakeholder | Stake | Voice in decision? |
|---|---|---|
| Engineering | bears implementation cost | yes |
| Product | impact ke timeline | input |
| Finance | infra cost | input |

## 6. What Success Looks Like (6 months)
- {{kriteria observable}}.

## 7. What Failure Looks Like (6 months)
- {{kriteria observable}}.

## 8. Out of Scope
- {{...}}.
```
