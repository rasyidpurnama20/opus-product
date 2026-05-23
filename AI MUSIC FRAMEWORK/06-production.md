# Stage 06 — Production → Production Plan

**Code:** `PRD` | **Output:** `PP-<track>-001`

## Purpose
Mengubah Sound Palette + Arrangement Map jadi **struktur project FL Studio yang rapi**: penamaan pattern, channel rack grouping, mixer routing, color coding, automation strategy. Stage ini yang membedakan project yang bisa di-revisit 6 bulan lagi vs project yang harus dibongkar dari nol.

## DoR
- [ ] Sound Palette `APPROVED`.

## DoD
- [ ] Naming convention pattern, channel, mixer track sudah jelas.
- [ ] Mixer routing tree (group / bus / send) didokumentasi.
- [ ] Automation lane strategy (per parameter, per section).
- [ ] Bounce v0.2.0 (rough mix dengan semua elemen Sound Palette).

---

## Prompt Template

```
1. ROLE
You are a producer who values FLP organization as much as the music itself.
You believe future-you should open the project and understand it in 30 seconds.

2. CONTEXT
DAW: FL Studio {{versi}}. Saya cenderung berantakan di project organization.

3. INPUT
- AM-{{slug}}-001: {{paste}}
- SP-{{slug}}-001: {{paste}}

4. TASK
- Sarankan naming convention: pattern, channel, mixer.
- Mixer routing tree: instrument → group → master.
- Automation strategy: parameter mana di-automate, di section mana, via clip atau Patcher.
- Color coding scheme.
- Tetapkan checkpoint render: bounce stem v0.2.0 sebelum mixing.

5. OUTPUT
06-production-plan.md.

6. CONSTRAINTS
- Naming harus konsisten dengan AM section name.
- Mixer routing tidak boleh melebihi 3 level (instrument → group → master).

7. ACCEPTANCE
- [ ] Naming convention 1 slide.
- [ ] Mixer routing diagram.
- [ ] Automation matrix (parameter × section).
```

---

## Artifact Template — `PP-<track>-001`

```markdown
# Production Plan — {{Track Title}}

| Field | Value |
|---|---|
| ID | PP-{{slug}}-001 |
| Status | DRAFT |
| Linked AM | AM-{{slug}}-001 |
| Linked SP | SP-{{slug}}-001 |

## 1. Naming Convention

### Patterns
`<NN>-<section>-<element>` — `01-intro-pad`, `02-verse1-drums`, `03-drop-lead`.

### Channel Rack
`[<lane>] <element> — <preset>` — `[DRM] Kick body — Vintage808`, `[BAS] Sub — Serum sine`.

### Mixer Tracks
`MX <NN> <name>` — `MX 01 Kick`, `MX 10 Drum BUS`, `MX 80 Master`.

## 2. Mixer Routing Tree
```
MX 01 Kick ──┐
MX 02 Snare ─┤
MX 03 Hat ───┼──► MX 10 DRUM BUS ──┐
MX 04 Perc ──┘                     │
                                   │
MX 11 Sub ───┐                     │
MX 12 MidBs ─┼──► MX 20 BASS BUS ──┤
MX 13 TopBs ─┘                     │
                                   │
MX 21 Rhodes ┐                     ├──► MX 70 MIX BUS ──► MX 80 MASTER
MX 22 Pad ───┴──► MX 30 CHORD BUS ─┤
                                   │
MX 31 Lead ──┐                     │
MX 32 Octv ──┼──► MX 40 LEAD BUS ──┤
MX 33 VoxCh ─┘                     │
                                   │
MX 50 Riser ─┐                     │
MX 51 Impact ┼──► MX 60 FX BUS ────┘
MX 52 Down ──┘

Sends:
- All BUS → MX 75 REVERB SEND (plate, decay 1.8s)
- All BUS → MX 76 DELAY SEND (1/8 dotted, feedback 30%)
```

## 3. Automation Matrix
| Parameter | Section(s) | Method |
|---|---|---|
| Pad LP filter cutoff | Intro→V1 | clip automation, open over 8 bars |
| Sidechain depth (Bass→Kick) | All | Patcher macro, manual override Drop2 first 4 bar |
| Reverb send (Lead) | Bridge | clip, increase to +6dB then back |
| Tape stop (Master) | end of Drop2 → Outro | Effector tape stop |
| Delay feedback | last bar before Drop | clip, briefly to 60% then snap back |

## 4. Color Coding
- Drums: red.
- Bass: orange.
- Chord/Pad: green.
- Lead/Hook: yellow.
- FX: purple.
- Vocal: blue.
- Master: black.

## 5. Checkpoints
- Bounce `v0.2.0-rough.wav` setelah Sound Palette terpasang, **belum** dimixing serius.
- Bounce stem `stems/v0.2.0/` (per group bus): drum.wav, bass.wav, chord.wav, lead.wav, fx.wav.

## 6. Hygiene Checklist
- [ ] Tidak ada channel "Sample 1" atau "Untitled".
- [ ] Tidak ada plugin di mixer yang bypass tapi dibiarkan.
- [ ] Pattern length konsisten (4/8/16).
- [ ] Tempo & key ditulis di project info.
- [ ] FLP saved dengan nama: `<slug>-v0.2.0.flp`.
```
