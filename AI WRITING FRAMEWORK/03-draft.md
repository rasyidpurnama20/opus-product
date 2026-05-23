# Stage 03 — Draft → First Draft

**Code:** `DR` | **Output:** `FD-<piece-slug>-001`

## Purpose
Tulis lengkap, jelek dulu boleh. Yang penting **selesai** dari hook ke conclusion. Editing nanti.

## DoD
- [ ] Semua section di outline ditulis lengkap.
- [ ] Code snippet teruji jalan (untuk technical writing).
- [ ] Tidak ada bracket `[TBD]` / `<<TODO>>` tertinggal.

## Prompt (per section, jangan satu prompt monster untuk seluruh tulisan)
```
ROLE: ghostwriter yang menjaga voice penulis. Saya akan kasih sample voice saya — pakai itu.
CONTEXT: saya nulis section {{S1}} dari outline.
INPUT:
- AB-{{slug}}-001: persona, voice & tone.
- OL-{{slug}}-001: outline section yang dimaksud.
- Sample voice saya: {{paste 1–2 paragraf tulisan saya yang lain}}.
TASK:
- Tulis draft section ini, panjang sesuai word budget di outline.
- Pakai code example yang sudah dirancang.
- Jaga voice (bukan terlalu formal, bukan AI-ish).
OUTPUT: section dalam Markdown, simpan sebagai 03-draft.md (append).
CONSTRAINTS:
- Hindari: "in conclusion", "delve into", "leveraging", "in this article we will explore".
- Hindari kalimat panjang > 30 kata.
- Tidak ada paragraf > 5 baris.
ACCEPTANCE:
- [ ] Word count ±15% dari budget.
- [ ] Voice match sample saya.
- [ ] Tidak ada AI-tells (over-formal, over-balanced).
```

## Working File Layout
```markdown
<!-- 03-draft.md -->
# {{Piece Title}}

<!-- HOOK -->
{{paragraf hook}}

<!-- THESIS -->
{{kalimat thesis di intro}}

## S1. The Problem
{{...}}

## S2. Why gather() Is Not Enough
{{...}}

## S3. Enter Task Groups
{{...}}

## S4. The Mental Model Shift
{{...}}

## S5. Migration Strategy
{{...}}

## Conclusion
{{...}}
```

## Anti-AI-Tells Quick Checklist
Hapus / rewrite saat draft kelihatan AI-generated:
- ❌ "Let's delve into..."
- ❌ "It's important to note that..."
- ❌ "In today's fast-paced world..."
- ❌ "On the one hand... on the other hand..." (over-balanced)
- ❌ Daftar yang selalu 3 item dengan struktur paralel sempurna.
- ❌ Setiap paragraf diakhiri dengan "this approach allows..."
- ❌ Kalimat pembuka selalu "Furthermore/Moreover/Additionally".

## Pomodoro Block
- 25 menit per section, 5 menit jeda.
- Tutup AI window selama 25 menit pertama (write own draft).
- 25 menit kedua: paste ke AI, minta improve sambil keep voice.
