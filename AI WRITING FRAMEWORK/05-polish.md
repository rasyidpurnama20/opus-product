# Stage 05 — Polish → Polish Pass

**Code:** `PO` | **Output:** `PP-<piece-slug>-001`

## Purpose
Detail final: typo, grammar, sentence flow, code snippet test, link check, headline final.

## DoD
- [ ] Spell check + grammar check pass.
- [ ] Setiap link diuji (200 OK).
- [ ] Setiap code snippet jalan (kalau technical).
- [ ] Headline final + meta description.
- [ ] Read-aloud test (sentence flow).

## Prompt
```
ROLE: copy-editor.
INPUT: draft post-edit (v2).
TASK:
- Spell + grammar check.
- Sentence flow: mana kalimat yang awkward? Saran rewrite minimal.
- Code snippet sanity check (komentar konsistensi, naming).
- Generate 5 alternatif headline (clickable tapi tidak clickbait).
- Generate 1 meta description ≤ 160 char.
- Link check: minta saya verify URL yang dipakai.
OUTPUT: 05-polish-notes.md.
CONSTRAINTS: jangan ubah voice / argument struktural.
ACCEPTANCE: spell/grammar pass, 5 headline, meta desc, code snippets reviewed.
```

## Template
```markdown
# Polish Notes — {{Piece Title}}

| Field | Value |
|---|---|
| ID | PP-{{slug}}-001 |
| Linked draft v2 | {{file}} |

## Spell / Grammar
- 4 typo fixed (paragraf 2, 7, 12, 19).
- 2 subject-verb agreement (paragraf 5, 14).

## Awkward Sentences (suggest rewrite)
| # | Original | Rewrite |
|---|---|---|
| 1 | "It is the case that task groups make this easier..." | "Task groups make this easier..." |
| 2 | "Due to the fact that the runtime allocates..." | "Because the runtime allocates..." |

## Code Snippets
- S1: ✅ jalan di Python 3.11, output sesuai narasi.
- S3: ✅, tapi tambahkan komentar `# raises ExceptionGroup if any task fails`.
- S5: typo `gather` di line 7 (capitalization).

## Headlines (5 alternatif)
1. "Stop Using asyncio.gather (Most of the Time)"
2. "Task Groups: Async Concurrency Yang Tidak Bocor"
3. "The Boring Reason Your Async Code Hangs"
4. "Async Yang Bisa Diandalkan: Pakai Task Group"
5. "Dari asyncio.gather ke TaskGroup: Migrasi 30 Menit"

**Recommended:** #3 (curiosity) atau #1 (provocative) — pilih sesuai platform.

## Meta Description
> "Async Python sering hang/leak karena gather() tidak punya scope. Task group memaksa lifetime task ke scope, mengeliminasi seluruh kelas bug. Cara migrasi 30 menit di dalam." (159 char)

## Final Read-Aloud
- [ ] Saya baca keras seluruh tulisan.
- [ ] Tidak ada kalimat yang bikin saya tersedak / kembali.
- [ ] Hook benar-benar menarik di kalimat pertama.
```
