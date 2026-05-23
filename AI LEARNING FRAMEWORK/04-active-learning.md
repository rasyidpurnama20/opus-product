# Stage 04 — Active Learning → Notes + Practice Log

**Code:** `AL` | **Output:** `NL-<topic-slug>-NNN` (per sesi)

## Purpose
Belajar aktif: tidak pasif menonton/baca, tapi membuat catatan dengan kata sendiri, latihan, dan recall.

## DoD per sesi
- [ ] Catatan dengan: 3–5 ide kunci dalam kalimat sendiri, 1+ pertanyaan terbuka, 1+ contoh konkret.
- [ ] Latihan / practice yang dieksekusi.
- [ ] Flashcard / Anki cards dibuat (3–5 per sesi).
- [ ] Recall pass: tutup catatan, jawab pertanyaan dari memori.

## Prompt (per sesi belajar)
```
ROLE: tutor sokratis yang menguji pemahaman lewat pertanyaan.
INPUT: ringkasan materi yang baru saya pelajari + catatan saya.
TASK:
- Cek pemahaman saya: ajukan 5 pertanyaan dari mudah ke sulit.
- Tunjukkan kesalahan / gap di catatan saya.
- Sarankan 2 latihan (problem solve) yang menerapkan konsep.
- Generate 5 flashcard (Q-A) cocok untuk Anki.
OUTPUT: feedback + flashcard.
CONSTRAINTS: jangan kasih jawaban dulu; biarkan saya jawab dulu.
ACCEPTANCE: 5 question, 2 exercise, 5 flashcard.
```

## Template per sesi
```markdown
# Notes Log — {{Topic}} / Session {{NNN}}

| Field | Value |
|---|---|
| ID | NL-{{slug}}-{{NNN}} |
| Date | {{...}} |
| Source | {{book ch / course module / paper}} |
| Duration | 45 min |

## 1. Key Ideas (in my own words)
- {{ide 1}}.
- {{ide 2}}.
- {{ide 3}}.

## 2. Concrete Example
{{contoh konkret yang saya buat sendiri, bukan dari sumber}}.

## 3. Open Questions
- {{Q1 yang belum terjawab.}}
- {{Q2 yang ingin saya gali lebih.}}

## 4. Practice Done
- Exercise X: {{deskripsi singkat + hasil}}.
- Exercise Y: {{...}}.

## 5. Flashcards
| Q | A |
|---|---|
| Apa beda X dan Y? | X menekankan ..., Y menekankan ... |
| Kapan pakai Z? | Ketika ... |
| ... | ... |

## 6. Recall Pass (closed-book)
- [ ] Saya bisa menjawab 5 pertanyaan AI di atas tanpa buka catatan.
- Score: {{4/5}}.
- Yang salah: {{...}} → review besok.

## 7. Connection to Earlier Sessions
- Konsep ini meneruskan {{NL-{{slug}}-{{MMM}}}} (subtopik X).
- Bertentangan / nuansa beda dengan {{...}} — perlu klarifikasi.
```
