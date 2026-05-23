# Example — Todo App (End-to-End)

Contoh ringkas penerapan framework untuk fitur kecil: **menambah & menyelesaikan todo item**.

Tujuannya menunjukkan bagaimana artifact saling rujuk dari Stage 01 → 08 (di sini hanya 01–05 dicontohkan untuk tetap ringkas).

```
01 VB-todo-001     ──►  02 PRD-todo-001 + US-todo-001
                              │
                              ▼
                        03 ARCH-todo-001 + ADR-todo-001
                              │
                              ▼
                        04 DM-todo-001 + OAS-todo-001 + UIS-todo-001
                              │
                              ▼
                        05 TB-todo-001
```

File:
- `vb-todo-001.md` — Vision Brief.
- `prd-todo-001.md` — Product Requirements + User Stories (digabung untuk ringkas).
- `arch-todo-001.md` — Architecture Doc + 1 ADR inline.
- `dm-todo-001.md` — Data Model + OpenAPI subset + UI Spec subset.
- `tb-todo-001.md` — Task Breakdown.
