# Stage 02 — Outline → Outline

**Code:** `OL` | **Output:** `OL-<piece-slug>-001`

## Purpose
Petakan struktur sebelum nulis kalimat lengkap. Outline mencegah tulisan loncat-loncat.

## DoD
- [ ] OL: hook, thesis, section list dengan tujuan, supporting evidence/example per section, conclusion + CTA, kasar word budget per section.

## Prompt
```
ROLE: editor yang ngotot tentang struktur.
INPUT: AB + ide kasar isi.
TASK:
- Generate hook (kalimat pembuka yang membuat persona mau lanjut baca).
- Tulis thesis (1 kalimat: yang dibuktikan oleh tulisan).
- Pecah jadi 3–6 section logis. Tiap section punya:
  - Sub-heading.
  - Tujuan (apa yang reader akan paham setelah section).
  - 1–3 bullet supporting points.
  - Contoh / data / code yang akan dipakai.
- Conclusion + CTA.
- Word budget per section (total ≤ panjang target).
OUTPUT: 02-outline.md.
CONSTRAINTS: bukan ToC ala buku — outline = peta argumen.
ACCEPTANCE: hook, thesis, section purposes, evidence per section, word budget.
```

## Template
```markdown
# Outline — {{Piece Title}}

| Field | Value |
|---|---|
| ID | OL-{{slug}}-001 |
| Linked AB | AB-{{slug}}-001 |
| Target word count | 1500 |

## Hook (≤ 50 words)
"Pernah punya kode async yang hang random tanpa bisa di-debug? Ini bukan kebetulan — ini structured-concurrency yang bocor."

## Thesis (1 sentence)
Pakai task group (`asyncio.TaskGroup` atau `trio.open_nursery()`) menggantikan `asyncio.gather()` mengubah async dari "harapan" jadi "kontrak" — yang mengeliminasi seluruh kelas bug yang umum.

## Sections

### S1. The Problem (~250 words)
- Tujuan: tunjukkan 3 jenis bug umum yang terjadi tanpa structured concurrency.
- Bullet:
  - Task lupa di-await → "fire and forget" yang silent fail.
  - Exception di salah satu task → tidak menghentikan yang lain.
  - Cancellation propagation gagal.
- Code example: minimal repro 10 baris.

### S2. Why gather() Is Not Enough (~200 words)
- Tujuan: jelaskan mengapa solusi populer (`asyncio.gather`) inadequate untuk bug di atas.
- Bullet: behaviour return_exceptions, no automatic cancel.

### S3. Enter Task Groups (~350 words)
- Tujuan: perkenalkan TaskGroup + nursery, kontras gagal-gracefully vs gather.
- Code example: same repro, with TaskGroup.

### S4. The Mental Model Shift (~300 words)
- Tujuan: explain "scope owns lifetime" → tidak ada task lepas dari scope.
- Diagram: scope as container.

### S5. Migration Strategy (~250 words)
- Tujuan: kalau codebase besar pakai gather, bagaimana refactor incrementally.
- Bullet: 3-step approach.

### S6. Conclusion + CTA (~150 words)
- Tujuan: rangkum, ajak reader coba di side project.
- CTA: "Try it minggu ini di 1 hot path. Reply / DM kalau hit edge case."

## Word Budget Total: ~1500
```
