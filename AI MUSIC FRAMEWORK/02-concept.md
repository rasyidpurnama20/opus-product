# Stage 02 — Concept → Track Brief

**Code:** `CON` | **Output:** `TB-<track>-001`

## Purpose
Menerjemahkan mood menjadi *narasi* track: bagaimana 3 menit ini mengalir, momen klimaks di mana, ending seperti apa. Tanpa narasi, arrangement gampang jadi "loop yang dipanjangin".

## DoR
- [ ] Mood Board `APPROVED`.

## DoD
- [ ] Track Brief memuat: log line, 3-act story, energy curve sketch, target durasi tepat, tonal center final.
- [ ] Setiap section punya tujuan emosional (bukan sekadar "verse 1").

---

## Prompt Template

```
1. ROLE
You are a senior film/score composer who thinks of every track as a narrative.

2. CONTEXT
Saya sudah punya Mood Board. Sekarang saya butuh story arc untuk track ini.

3. INPUT
- MB-{{slug}}-001:
{{paste mood board}}

4. TASK
Bantu saya menulis Track Brief:
- Tulis log line (1 kalimat) yang menangkap perjalanan track.
- Pecah jadi 3 act dengan emosi target tiap act.
- Sketsa energy curve (skala 1–10 per section, total ~6–8 section).
- Tetapkan durasi target dan section count.
- Pilih tonal center final dari kandidat MB.
- Identifikasi "moment" (klimaks, drop, breakdown) dan kapan terjadi.

5. OUTPUT
Markdown 02-track-brief.md.

6. CONSTRAINTS
- Tidak menulis chord progression / melodi.
- Section name pakai bahasa fungsional (Intro, Build, Drop, Bridge, Outro), bukan teknis FL Studio (Pattern 3).

7. ACCEPTANCE
- [ ] Log line max 25 kata.
- [ ] 3 act dengan target emosi.
- [ ] Energy curve dengan angka per section.
- [ ] 1 "moment" eksplisit (di bar berapa kira-kira).
```

---

## Artifact Template — `TB-<track>-001`

```markdown
# Track Brief — {{Track Title}}

| Field | Value |
|---|---|
| ID | TB-{{slug}}-001 |
| Status | DRAFT |
| Linked MB | MB-{{slug}}-001 |

## 1. Log Line
> {{1 kalimat menjelaskan emosi & jalan cerita track.}}

## 2. Three-Act Structure
| Act | Section(s) | Emotional Goal |
|---|---|---|
| Act I — Setup | Intro, Verse 1 | menanam mood: tenang tapi gelisah |
| Act II — Conflict | Pre-chorus, Drop, Bridge | meningkat → klimaks emosi |
| Act III — Resolution | Verse 2, Outro | luruh, refleksi |

## 3. Section Plan
| # | Section | Bars | Energy (1–10) | Purpose |
|---|---|---|---|---|
| 1 | Intro | 8 | 2 | tanam motif |
| 2 | Verse 1 | 16 | 4 | masukin kit minimal |
| 3 | Pre-chorus | 8 | 6 | tension |
| 4 | Drop | 16 | 9 | klimaks pertama |
| 5 | Verse 2 | 16 | 5 | dynamic dip |
| 6 | Bridge | 8 | 8 | reframe |
| 7 | Drop 2 | 16 | 10 | klimaks final |
| 8 | Outro | 8 | 3 | resolve |

Total: ~96 bars @ {{BPM}} ≈ {{durasi menit:detik}}.

## 4. Tonal Center
- Final key: {{F minor}}.
- Modal flavor: {{aeolian dengan flirt ke dorian di bridge}}.

## 5. Signature Moment
- "Moment" utama: bar {{49}} (Drop 2) — semua elemen lepas, vocal chop pertama muncul.

## 6. References Mapped
| Section | Reference (track + timestamp) |
|---|---|
| Intro | {{Artist - Track @ 0:00–0:15}} |
| Drop | {{...}} |

## 7. Open Questions
- {{...}}
```
