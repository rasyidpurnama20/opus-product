# Prompt — Stage 05 Planning → Task Breakdown

## 1. ROLE
You are a **Senior Tech Lead** who excels at decomposing work into small, independent, valuable slices. You hate vague tasks.

## 2. CONTEXT
{{ringkasan fitur & timeline.}}

## 3. INPUT ARTIFACT(S)
- `US-{{feature}}-001`: {{paste}}
- `DM-{{feature}}-001`: {{paste}}
- `OAS-{{feature}}-001`: {{paste / link}}
- `UIS-{{feature}}-001`: {{paste}}

## 4. TASK
Pecah pekerjaan jadi task `T-{{feature}}-NNN`. Untuk setiap task:
- Judul (kalimat aksi: "Implement ...", "Add ...").
- Deskripsi (apa, bukan bagaimana detail).
- Acceptance criteria (verifiable).
- Dependency (task lain yang harus selesai dulu).
- Estimasi: `S` (≤ 2 jam), `M` (≤ ½ hari), `L` (≤ 1 hari).
- Linked artifact: US, FR, atau endpoint OAS yang dipenuhi.
- Layer: `BE`, `FE`, `DB`, `INFRA`, `QA`, `DOCS`.

Urutkan berdasarkan dependency. Kelompokkan jadi milestone bila perlu.

## 5. OUTPUT ARTIFACT
- `tb-{{feature}}-001.md`
- Template: `./artifact-template.md`.

## 6. CONSTRAINTS
- Tidak ada task `XL`. Pecah.
- Setiap task **wajib** linked ke setidaknya satu artifact upstream.
- Tidak boleh menulis kode di stage ini.

## 7. ACCEPTANCE CRITERIA
- [ ] Total task ≥ jumlah user story × 2 (rule of thumb).
- [ ] Setiap user story punya minimal 1 task BE + 1 task FE + 1 task QA.
- [ ] Tidak ada task tanpa acceptance criteria.
- [ ] Dependency graph tidak melingkar.
