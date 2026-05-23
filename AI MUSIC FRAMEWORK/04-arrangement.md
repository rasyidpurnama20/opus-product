# Stage 04 — Arrangement → Arrangement Map

**Code:** `ARR` | **Output:** `AM-<track>-001`

## Purpose
Memetakan **bar per bar** apa yang terjadi: kapan elemen masuk, kapan keluar, di mana fill, di mana riser, di mana drop. Tanpa peta ini, arrangement berkembang dengan "feeling" dan biasanya panjang sebelah.

## DoR
- [ ] Melodic Sketch `APPROVED`.

## DoD
- [ ] Tabel bar-by-bar dengan minimal 6 lane (Drum, Bass, Chord, Lead, FX, Vocal/Lead Hook).
- [ ] Energy curve grafik (bisa ASCII).
- [ ] Tiap section punya transition technique (riser, drop-out, fill, downlifter).

---

## Prompt Template

```
1. ROLE
You are an arranger / track-builder for {{genre}}. You think in bars.

2. CONTEXT
Saya sudah punya sketch. Saya butuh arrangement final (bar-by-bar) sebelum sound design.

3. INPUT
- TB: {{paste}}
- MS: {{paste}}

4. TASK
- Buat tabel bar-by-bar untuk seluruh track (96 bar).
- Lane minimal: Drum, Bass, Chord, Lead, FX, Vocal/Hook, Texture.
- Mark "ON / OFF / FILL / SUSTAIN / EVOLVE" tiap lane per bar (atau per 4 bar).
- Tetapkan transition technique antar section.
- Sinkronkan dengan energy curve di TB; flag jika ada konflik.

5. OUTPUT
04-arrangement-map.md.

6. CONSTRAINTS
- Tidak menentukan plugin/preset.
- Setiap section panjangnya kelipatan 4 bar (kecuali sengaja odd).

7. ACCEPTANCE
- [ ] Energy curve sketch terisi.
- [ ] Tiap section punya transition method.
- [ ] Total bar match TB.
```

---

## Artifact Template — `AM-<track>-001`

```markdown
# Arrangement Map — {{Track Title}}

| Field | Value |
|---|---|
| ID | AM-{{slug}}-001 |
| Status | DRAFT |
| Linked TB | TB-{{slug}}-001 |
| Linked MS | MS-{{slug}}-001 |
| Total bars | 96 |

## 1. Energy Curve
```
10 |              ░░░░          ░░░░░░░░
 8 |        ░░░░░░░░░░░░  ░░░░░░░░░░░░░░
 6 |    ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
 4 |  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
 2 |░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
   +-------------------------------------
     INT  V1  PRE  DROP  V2  BR  DROP2 OUT
```

## 2. Bar Map (per 4 bar block)

| Block (bars) | Section | Drum | Bass | Chord | Lead | FX | Hook |
|---|---|---|---|---|---|---|---|
| 1–4 | Intro | OFF | OFF | SUSTAIN (pad) | OFF | air FX | OFF |
| 5–8 | Intro | KICK only | ROOT only | SUSTAIN | OFF | reverse cymbal at b8 | OFF |
| 9–16 | Verse 1 | half-time kit | ROOT | RHYTHM | EVOLVE motif | — | OFF |
| 17–24 | Verse 1 | + perc | + 5th | RHYTHM | hook half-statement | rise at b23-24 | half |
| 25–32 | Pre-chorus | full kit, snare roll b32 | walking | TENSION | OFF | riser b29-32 | OFF |
| 33–48 | Drop | full + claps | octave punch | RHYTHM | full hook | impact b33 | full |
| 49–64 | Verse 2 | minimal | ROOT | RHYTHM | hook variation | drop-out b48→b49 | full |
| 65–72 | Bridge | break | pedal Bb | borrowed | counter-melody | downlifter b72 | OFF |
| 73–88 | Drop 2 | + tom fills | octave + slide | RHYTHM | hook + harmony | impact + air | full + ad-lib |
| 89–96 | Outro | tail | OFF | SUSTAIN | echo hook | reverb tail | OFF |

## 3. Transitions
| From → To | Technique |
|---|---|
| Intro → V1 | reverse cymbal + kick on b9 |
| V1 → Pre | snare roll last 2 bars |
| Pre → Drop | white-noise riser + impact |
| Drop → V2 | hard drop-out, vocal echo tail |
| V2 → Bridge | filter sweep down |
| Bridge → Drop2 | downlifter + 2-beat silence + impact |
| Drop2 → Outro | filter cutoff + reverb wash |

## 4. Risk Flags
- R1: Drop2 mungkin terlalu mirip Drop1 → mitigasi: tambah counter-melody di harmony.
- R2: Bridge break bisa kehilangan momentum → mitigasi: pedal point + snare ghost notes.

## 5. FL Studio Note
- Marker per section pakai warna: Intro=biru, Verse=hijau, Pre=kuning, Drop=merah, Bridge=ungu, Outro=abu.
- Pattern di-color sesuai instrument family.
```
