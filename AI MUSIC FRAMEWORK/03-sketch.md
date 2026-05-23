# Stage 03 — Sketch → Melodic Sketch

**Code:** `SKT` | **Output:** `MS-<track>-001`

## Purpose
Menetapkan **musik mentah** yang akan jadi tulang track: chord progression utama, melodic hook, bass motion. Sketch ini biasanya cukup di-realisasi dengan piano + drum sederhana di FL Studio.

## DoR
- [ ] Track Brief `APPROVED`.

## DoD
- [ ] Chord progression utama (untuk section A & B) dengan notasi (mis. `Fm – Db – Bbm7 – Eb`).
- [ ] Melodic hook ditulis (notasi atau rhythmic shape + interval contour).
- [ ] Bass motion strategy (root / walking / pedal).
- [ ] Demo piano roll di FL Studio diekspor sebagai MIDI + audio sketch (bounce v0.1.0).

---

## Prompt Template

```
1. ROLE
You are a senior composer fluent in jazz harmony and modern pop voicing.

2. CONTEXT
Saya butuh sketch musikal untuk track berikut.

3. INPUT
- MB: {{ringkasan}}
- TB: {{paste track brief}}

4. TASK
Berdasarkan TB:
- Sarankan 3 alternatif chord progression untuk section A (Verse) dan section B (Drop/Chorus).
- Setiap progression: 4–8 bar, notasi roman numeral + chord symbol.
- Untuk progression terpilih (saran Anda), berikan voicing tip (close/open, inversion).
- Sarankan melodic hook contour (rhythmic + interval shape, bukan notasi pasti).
- Strategi bass motion per section.
- Modulasi/borrowed chord di Bridge (kalau ada).

5. OUTPUT
03-melodic-sketch.md.

6. CONSTRAINTS
- Tetap di tonal center yang ditentukan TB.
- Tidak boleh menyarankan plugin / synth (itu stage berikutnya).

7. ACCEPTANCE
- [ ] 3 alternatif tiap section.
- [ ] Bass strategy eksplisit.
- [ ] Melodic hook punya kontur (naik/turun + interval kunci).
```

---

## Artifact Template — `MS-<track>-001`

```markdown
# Melodic Sketch — {{Track Title}}

| Field | Value |
|---|---|
| ID | MS-{{slug}}-001 |
| Status | DRAFT |
| Linked TB | TB-{{slug}}-001 |
| Key | F minor |
| BPM | 92 |

## 1. Chord Progressions

### Verse — chosen
| Bar | Chord | Roman | Voicing tip |
|---|---|---|---|
| 1 | Fm9 | i9 | close, omit 5 |
| 2 | Db maj7 | bVI maj7 | open, +9 |
| 3 | Bbm7 | iv7 | drop-2 |
| 4 | Eb sus2 → Eb | bVII | suspended ¾, resolve |

Alternatives considered:
- B: i – bIII – iv – v (more melancholic, rejected — terlalu mirip referensi).
- C: i – bVI – bVII – v (too anthemic).

### Drop — chosen
{{...}}

### Bridge — borrowed chord
Pinjam ii (Gm7b5) dari F locrian untuk 2 bar tension sebelum kembali ke i.

## 2. Melodic Hook
- Contour: turun stepwise 3 nada, lompat naik 5, turun stepwise 4 nada.
- Rhythmic shape: dotted-eighth + sixteenth + quarter (dotted feel).
- Range: F4–C5.
- Repeats every 4 bar.

## 3. Bass Motion
| Section | Strategy |
|---|---|
| Verse | root + 5, sustained |
| Pre-chorus | walking quarter notes |
| Drop | root + octave punch on beat 1 & 3 |
| Bridge | pedal point on Bb |

## 4. Counter-Melody / Pads
- Counter-melody di Drop: arpeggio descending pada bar 3-4 dari hook.
- Pad: long sustained, voicing 1–3–5–9.

## 5. FL Studio Sketch
- File: `flp/sketch-v0.1.0.flp`.
- Bounce: `bounces/v0.1.0-sketch.wav` (piano + clap, no FX).
- Notes: tempo 92, 8-bar verse + 8-bar drop loop.

## 6. Open Questions
- Apakah Bridge perlu modulation key, atau cukup borrowed chord?
```
