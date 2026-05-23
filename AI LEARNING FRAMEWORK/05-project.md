# Stage 05 — Project → Capstone Brief

**Code:** `PJ` | **Output:** `CP-<topic-slug>-001`

## Purpose
Mengkristalkan pembelajaran lewat **project nyata**. Tanpa project, ilmu menguap dalam 3 bulan.

## DoD
- [ ] Capstone Brief memuat: project description, outcome bukti, scope, technical stack, milestone, deliverable publik.

## Prompt
```
ROLE: mentor project untuk pemula-mid yang baru selesai belajar topik.
INPUT: LG + TM + skill yang sudah dikuasai (dari NL log).
TASK:
- Sarankan 3 ide project dengan complexity berbeda.
- Untuk yang dipilih: scope, deliverable, success metric, risiko.
- Pecah jadi 4–6 milestone (1–2 minggu masing-masing).
- Sarankan publik artifact: GitHub, blog post, video demo.
OUTPUT: 05-capstone.md.
CONSTRAINTS: project harus selesai dalam waktu yang tersisa di Study Plan.
ACCEPTANCE: scope realistic, milestone ada, deliverable publik.
```

## Template
```markdown
# Capstone Brief — {{Topic}} / {{Project Name}}

| Field | Value |
|---|---|
| ID | CP-{{slug}}-001 |
| Linked LG | LG-{{slug}}-001 |
| Estimated time | 4 weeks |

## 1. Description
{{Apa yang akan dibangun, untuk siapa, masalah apa.}}

## 2. Outcome Evidence
- Public repo / artifact: {{URL}}.
- Demo: {{video / live link}}.
- Blog post: 800–1500 words explaining what you built and learned.

## 3. Scope
- **In:** {{...}}
- **Out:** {{...}}

## 4. Stack
- Language: {{...}}
- Library: {{...}}
- Infra: {{...}}

## 5. Milestones
| # | Week | Goal | Deliverable |
|---|---|---|---|
| 1 | 1 | Skeleton + main loop | repo init + first commit |
| 2 | 2 | Core feature 1 | branch + PR |
| 3 | 3 | Feature 2 + tests | release v0.1 |
| 4 | 4 | Polish + write blog | release v1.0 + post live |

## 6. Risks
- {{risiko 1}} → mitigasi.

## 7. Public Sharing
- [ ] GitHub README polished.
- [ ] LICENSE file.
- [ ] Blog post drafted by week 4.
- [ ] Share di komunitas: {{discord / reddit / linkedin}}.
```
