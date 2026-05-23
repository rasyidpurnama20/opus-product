# Stage 02 — Topic Map → Topic Map

**Code:** `TM` | **Output:** `TM-<topic-slug>-001`

## Purpose
Memetakan keseluruhan topik, identifikasi resource bagus, urutan belajar yang masuk akal.

## DoD
- [ ] TM memuat: tree subtopik, resource per subtopik (book/course/paper/blog), prasyarat antar subtopik, estimasi waktu, "must vs nice-to-know".

## Prompt
```
ROLE: kurator pendidikan yang tahu beda buku bagus vs hype.
INPUT: LG-{{slug}}-001 + level saya saat ini.
TASK:
- Pecah topik jadi pohon subtopik 2–3 level.
- Untuk tiap subtopik: 1–3 resource terbaik (sebut: jenis, judul, author, tahun, gratis/berbayar).
- Tandai "must" vs "nice-to-know".
- Susun dependency: subtopik mana harus didahulukan.
- Estimasi waktu kasar per subtopik.
OUTPUT: 02-topic-map.md.
CONSTRAINTS: TIDAK menyarankan resource yang Anda tidak yakin valid (tandai [VERIFY]).
ACCEPTANCE: tree 2+ level, resource per subtopik, prereq mapping, time estimates.
```

## Template
```markdown
# Topic Map — {{Topic}}

| Field | Value |
|---|---|
| ID | TM-{{slug}}-001 |
| Status | DRAFT |
| Linked LG | LG-{{slug}}-001 |

## 1. Subtopic Tree
- Foundation
  - {{...}} — must
  - {{...}} — must
- Intermediate
  - {{...}} — must
  - {{...}} — nice
- Advanced
  - {{...}} — nice
  - {{...}} — nice

## 2. Resources
| Subtopic | Resource | Type | Author | Year | Free? | Verified? |
|---|---|---|---|---|---|---|
| Foundation/X | "Book Title" | book | {{...}} | 2023 | yes | ✅ |
| Foundation/Y | "Course Name" | video course | {{...}} | 2024 | $$ | ✅ |
| Intermediate/Z | paper "..." | paper | {{...}} | 2022 | yes | [VERIFY] |

## 3. Dependency Graph
```
Foundation/X → Intermediate/Z
Foundation/Y → Intermediate/W
Intermediate/Z + Intermediate/W → Advanced/V
```

## 4. Time Estimate
| Subtopic | Hours |
|---|---|
| Foundation/X | 12 |
| Foundation/Y | 8 |
| ... | ... |
| **Total** | **80** |

## 5. Recommended Order
1. Foundation/X
2. Foundation/Y
3. Intermediate/Z
4. ...
```
