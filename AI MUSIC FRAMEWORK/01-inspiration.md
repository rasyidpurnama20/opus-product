# Stage 01 — Inspiration → Mood Board

**Code:** `INS` | **Output:** `MB-<track>-001`

## Purpose
Menangkap "rasa" yang ingin Anda ciptakan sebelum menyentuh piano roll. Output stage ini adalah landasan kreatif untuk semua keputusan setelahnya.

## DoR
- [ ] Anda punya minimal 1 ide samar (mood, momen, kisah, image).

## DoD
- [ ] Mood Board memuat: mood adjektiva, 3+ track referensi, BPM range, key candidate, instrumentation feel, target audience, target use-case (sync? streaming? live?).
- [ ] Tidak ada melodi/chord spesifik di stage ini.

---

## Prompt Template

```
1. ROLE
You are a senior music director with deep crate-digging experience across genres.
You are obsessive about mood-fit before notes.

2. CONTEXT
Saya sedang menggarap track baru. Background saya: {{producer FL Studio, genre yang biasa Anda buat, level skill}}.

3. INPUT
- Ide samar: {{kalimat / momen / mood / image}}.
- Referensi awal (jika ada): {{judul-artist / link / playlist}}.
- Konteks penggunaan: {{personal release / sync brief / client / latihan}}.
- Constraint: {{deadline, durasi target, vocal/instrumental, dst}}.

4. TASK
Bantu saya membentuk Mood Board:
- Ekstrak 5–7 mood adjektiva dari ide saya.
- Sarankan 5 track referensi yang menangkap mood tsb (dari era/genre yang berbeda agar tidak bias).
- Sarankan range BPM yang masuk akal beserta alasan.
- Sarankan 2–3 candidate key (major/minor/modal) dengan karakter masing-masing.
- Sarankan instrumentation feel (akustik / hybrid / electronic / orchestral / lo-fi).
- Identifikasi 2 risiko mood drift (mis. terlalu mirip referensi X).

5. OUTPUT
Markdown mengikuti template di bawah, simpan sebagai 01-mood-board.md.

6. CONSTRAINTS
- Tidak menulis akor/melodi.
- Referensi harus track yang benar-benar ada (jangan halusinasi judul).
- BPM harus angka, key harus notasi musik standar.

7. ACCEPTANCE
- [ ] 5–7 mood adjektiva.
- [ ] Minimal 5 referensi dengan artist + judul + alasan.
- [ ] BPM range + key candidates dengan justifikasi.
- [ ] Tidak ada saran melodi spesifik.
```

---

## Artifact Template — `MB-<track>-001`

```markdown
# Mood Board — {{Track Title (working title)}}

| Field | Value |
|---|---|
| ID | MB-{{slug}}-001 |
| Status | DRAFT |
| Date | {{YYYY-MM-DD}} |

## 1. Origin
{{Kalimat / momen / image yang memicu ide ini.}}

## 2. Mood Adjectives
nostalgic · cinematic · warm · restless · hopeful · {{...}}

## 3. Target Use-Case
- {{streaming release / sync ke film / portfolio / latihan / brief client}}.

## 4. Reference Tracks
| # | Artist — Title | Why it fits | What to borrow | What to avoid |
|---|---|---|---|---|
| 1 | {{...}} | {{...}} | tempo feel, drum bus | terlalu sad |
| 2 | | | | |
| 3 | | | | |

## 5. Tempo & Key
| Field | Value | Reason |
|---|---|---|
| BPM range | 88–96 | half-time hip-hop feel + ruang untuk groove |
| Key candidate 1 | F minor | dark warmth |
| Key candidate 2 | Bb dorian | tension positif |

## 6. Instrumentation Feel
- {{hybrid acoustic + analog synths + tape hiss}}.

## 7. Constraints
- Durasi: {{2:30–3:30}}.
- Vocal: {{ada / instrumental}}.
- Deadline: {{...}}.

## 8. Mood Drift Risks
- R1: {{...}} → mitigasi: {{...}}.
- R2: {{...}}.

## 9. Open Questions
- {{...}}
```
