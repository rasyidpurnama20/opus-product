# Stage 05 — Sound Design → Sound Palette

**Code:** `SND` | **Output:** `SP-<track>-001`

## Purpose
Menetapkan instrumen, preset, dan layering strategy untuk tiap lane di Arrangement Map. Tujuan: setiap suara punya peran sonik (frequency band + transient role + stereo zone) yang berbeda agar mix tidak collide.

## DoR
- [ ] Arrangement Map `APPROVED`.

## DoD
- [ ] Tiap lane punya: instrumen utama, plugin, preset family, frequency target, transient role, stereo zone.
- [ ] Konflik frequency dipetakan dan diselesaikan dengan EQ carving / re-pitching.

---

## Prompt Template

```
1. ROLE
You are a sound designer and producer who plans the sonic real-estate before recording.

2. CONTEXT
Saya kerja di FL Studio. Stock plugins yang biasa saya pakai: {{Sytrus, Harmor, FLEX, Serum, Pigments, Kontakt, Vital, dst}}. Sample library: {{...}}.

3. INPUT
- AM-{{slug}}-001:
{{paste arrangement map}}
- MB instrumentation feel: {{...}}.

4. TASK
- Untuk tiap lane (Drum, Bass, Chord, Lead, FX, Hook, Texture), sarankan instrumen utama + 1 alternatif.
- Tetapkan layering: berapa layer, peran tiap layer (sub / body / attack / air).
- Petakan frequency target tiap layer (sub <60, low 60–200, low-mid 200–500, mid 500–2k, hi-mid 2k–6k, air 6k+).
- Tetapkan stereo zone (mono / center / wide / hard L/R).
- Identifikasi 3 potensi frequency clash & cara hindari (EQ carve, sidechain, re-pitch, alternatif preset).

5. OUTPUT
05-sound-palette.md.

6. CONSTRAINTS
- Pakai plugin yang user sebut.
- Tidak boleh "tambahin reverb biar megah" tanpa peran spesifik.

7. ACCEPTANCE
- [ ] Tiap lane punya 1 instrumen utama + 1 alternatif.
- [ ] Tiap layer punya frequency target.
- [ ] 3+ potensi clash teridentifikasi & ada mitigasi.
```

---

## Artifact Template — `SP-<track>-001`

```markdown
# Sound Palette — {{Track Title}}

| Field | Value |
|---|---|
| ID | SP-{{slug}}-001 |
| Status | DRAFT |
| Linked AM | AM-{{slug}}-001 |

## 1. Lane × Layer Matrix

### Drum
| Layer | Role | Plugin / Sample | Freq Target | Stereo | Notes |
|---|---|---|---|---|---|
| Kick — sub | sub body | FLEX 808 sub | 40–60 Hz | mono | sidechain ke pad |
| Kick — body | thump | sample (Vintage Drum) | 80–120 Hz | mono | tune ke F |
| Kick — click | transient | Drumaxx | 3–5 kHz | mono | high-pass 1k |
| Snare — body | tone | sample | 180–250 Hz | center | parallel comp |
| Snare — top | snap | layered clap | 5–8 kHz | center | |
| Hat — closed | groove | sample | 8–12 kHz | LR alt | swing 16% |
| Perc | texture | shaker pack | 3–8 kHz | wide | sidechain to kick |

### Bass
| Layer | Role | Plugin | Freq | Stereo |
|---|---|---|---|---|
| Sub | sub | Serum (sine) | 30–80 Hz | mono |
| Mid bass | body | Sytrus saw | 100–400 Hz | mono center |
| Top bass | grit (drop only) | Harmor distortion | 800–2k | center |

### Chord
| Layer | Role | Plugin | Freq | Stereo |
|---|---|---|---|---|
| Rhodes | warmth | Kontakt: Scarbee Rhodes | 200–2k | wide |
| Pad | air | Pigments grain | 500 Hz–4k + air | wide |

### Lead / Hook
| Layer | Role | Plugin | Freq | Stereo |
|---|---|---|---|---|
| Lead synth | melody | Vital pluck | 1–4k | center |
| Octave-up layer | shimmer | Serum sine | 4–8k | wide |
| Vocal chop hook | character | Harmor resynth | 500 Hz–6k | center |

### FX
| Layer | Role | Plugin | Freq |
|---|---|---|---|
| Riser | tension | white noise + filter open | 200 Hz–10k sweep |
| Impact | drop hit | Kontakt cinematic hit | 50–8k |
| Reverse cymbal | upbeat | sample | 3–14k |
| Downlifter | bridge transition | Krotos / Vital | broad |

## 2. Frequency Conflict Map
| Range | Lanes that compete | Resolution |
|---|---|---|
| 60–120 Hz | Kick body × Sub Bass | sidechain bass to kick (10ms attack, 80ms release) |
| 200–400 Hz | Mid Bass × Rhodes | EQ carve Rhodes -3dB @ 250 Hz, narrow Q |
| 5–8 kHz | Hat × Snare top × Air Lead | hat duck on snare, lead high-shelf -2dB |

## 3. Macro / Automation
- Filter cutoff macro per section (controlled by mod wheel / Patcher).
- Sidechain ducking bypass selama Drop2 first 4 bar untuk full body.

## 4. Stem Plan
| Stem | Channels grouped | Sample rate |
|---|---|---|
| Drums | kick, snare, hat, perc | 48k/24bit |
| Bass | sub + mid + top | 48k/24bit |
| Chord | rhodes + pad | 48k/24bit |
| Lead | hook + counter | 48k/24bit |
| FX | riser, impact, etc | 48k/24bit |
```
