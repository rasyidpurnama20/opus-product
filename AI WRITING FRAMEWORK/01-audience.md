# Stage 01 — Audience → Audience Brief

**Code:** `AU` | **Output:** `AB-<piece-slug>-001`

## Purpose
Identifikasi pembaca tunggal yang dituju — usia, level, masalah, "apa yang akan mereka lakukan setelah baca".

## DoD
- [ ] AB: persona target (1 orang konkret), pre-knowledge, masalah yang mereka cari solusinya, "after-read action", platform, panjang target, deadline.

## Prompt
```
ROLE: editor yang ngotot tentang audience clarity.
CONTEXT: saya akan menulis {{tipe konten: blog/doc/thread/proposal}}.
INPUT: ide kasar saya.
TASK:
- Reformulasikan target reader jadi 1 persona konkret (umur, role, level, konteks pemakaian).
- Identifikasi: apa yang mereka tahu sebelum baca, apa masalah yang mereka cari solusinya.
- Tetapkan after-read action 1 kalimat ("setelah baca, mereka akan...").
- Saran panjang dan platform.
OUTPUT: 01-audience.md.
CONSTRAINTS: bukan "general developer audience" — terlalu vague.
ACCEPTANCE: persona spesifik, after-read action konkret.
```

## Template
```markdown
# Audience Brief — {{Piece Title}}

| Field | Value |
|---|---|
| ID | AB-{{slug}}-001 |
| Format | blog post / doc / thread / proposal |
| Platform | personal blog / Medium / LinkedIn / company docs |
| Length | ~1500 words |

## Persona
**Reader:** Mid-level Python developer, 28, 4 years experience, mostly worked on REST API at fintech, sekarang lagi explore async patterns, baca blog di malam hari setelah anak tidur.

## Pre-Knowledge (assumed)
- Sudah paham async/await syntax.
- Familiar dengan asyncio.
- Belum pernah pakai trio / structured concurrency.

## Pain (what they're searching)
"Mengapa kode async saya leak task / hang random / susah di-debug?"

## After-Read Action
"Setelah baca, mereka tahu kapan pakai task group dan akan mencoba di project sampingan minggu depan."

## Voice & Tone
- Personal, bukan korporat.
- Boleh casual ("eh", "btw"), tapi jaga teknis akurat.
- Kalimat pendek, paragraf max 4 baris.

## Constraints
- Tidak boleh > 1800 kata (audience baca di malam, attention span pendek).
- Setiap section punya 1 code snippet runnable.
- Headline harus punya "1 thing they'll learn".
```
