# Stage 07 — Mixing → Mix Notes

**Code:** `MIX` | **Output:** `MN-<track>-001`

## Purpose
Membuat balance, ruang, dan kedalaman antar elemen sehingga track siap di-master. Mixing **bukan** stage untuk fix arrangement.

## DoR
- [ ] Production Plan `APPROVED` & rough bounce `v0.2.0` ada.
- [ ] Tidak ada elemen baru yang ditambahkan setelah stage ini (kecuali ada keputusan eksplisit kembali ke stage 04/05).

## DoD
- [ ] Mix Notes memuat: gain staging plan, EQ subtraction tree, compression strategy, time-based FX, automation final, reference comparison.
- [ ] Bounce `v0.3.0-mix.wav` dengan headroom **-6 dB** di master (no limiter on master saat mixing).
- [ ] Pass A/B test: mix listenable di laptop speaker, headphone, mobile phone.

---

## Prompt Template

```
1. ROLE
You are a mix engineer for {{genre}}, with strong reference-based mixing discipline.

2. CONTEXT
Saya kerja di FL Studio. Saya cenderung over-EQ / over-compress. Saya butuh struktur.

3. INPUT
- AM, SP, PP: {{paste ringkasan}}
- Reference track final (untuk frequency & loudness target): {{Artist - Track}}.
- Bounce v0.2.0 saya: {{ringkasan: kicked terlalu boomy, lead tipis, dst.}}

4. TASK
- Gain staging: target VU per group bus & master pre-limiter.
- EQ tree: per element, subtractive cuts dulu, lalu boost.
- Compression: ratio + attack + release per element.
- Time FX: reverb (per kategori: short/medium/plate/hall), delay (per beat division).
- Automation final.
- Reference comparison checklist.

5. OUTPUT
07-mix-notes.md.

6. CONSTRAINTS
- Tidak boleh limit di master selama stage mix (itu mastering).
- Tidak boleh saran "tambah plugin X" tanpa peran sonik spesifik.
- Setiap saran EQ punya frequency + Q + dB + reason.

7. ACCEPTANCE
- [ ] Master peak ≤ -6 dBFS.
- [ ] EQ moves semua punya alasan (carve / shape / fix).
- [ ] Reference comparison memuat 3 metrik (low end, mid clarity, top air).
```

---

## Artifact Template — `MN-<track>-001`

```markdown
# Mix Notes — {{Track Title}}

| Field | Value |
|---|---|
| ID | MN-{{slug}}-001 |
| Status | DRAFT |
| Linked PP | PP-{{slug}}-001 |
| Reference | {{Artist - Track}} |

## 1. Gain Staging
| Bus | Target peak | RMS approx |
|---|---|---|
| MX10 Drum | -8 dBFS | -14 |
| MX20 Bass | -10 dBFS | -16 |
| MX30 Chord | -14 dBFS | -20 |
| MX40 Lead | -12 dBFS | -18 |
| MX60 FX | -16 dBFS | -22 |
| MX80 Master | -6 dBFS | — |

## 2. EQ Tree
### Kick body (MX01)
- HPF 30 Hz, 12 dB/oct.
- Cut 250 Hz (Q 1.0) -3 dB — boomy.
- Boost 80 Hz (Q 0.7) +1.5 dB — body.
- Boost 4 kHz (Q 1.0) +1 dB — click.

### Sub bass (MX11)
- HPF 28 Hz.
- Cut 350 Hz -4 dB — mud.
- LPF 200 Hz, 24 dB/oct — keep sub clean.

### Rhodes (MX21)
- HPF 120 Hz.
- Cut 250 Hz -3 dB — make space for bass.
- Wide stereo via Fruity Stereo Shaper at 130%.

### Lead (MX31)
- HPF 200 Hz.
- Cut 1.2 kHz -2 dB — nasal.
- Air shelf 12 kHz +1 dB.

(... lanjutkan untuk semua channel ...)

## 3. Compression
| Channel | Comp | Ratio | Attack | Release | Threshold (gr) |
|---|---|---|---|---|---|
| Kick | Fruity Limiter (clip mode) | — | — | — | -2 dB peak |
| Snare | OTT (low) | — | — | — | -3 dB |
| Drum BUS | Fruity Compressor | 2:1 | 30 ms | 80 ms | 2–3 dB GR |
| Bass | Multiband (Maximus 3 band) | per band | per band | per band | low 3dB |
| Vocal/Lead | Fruity Compressor | 4:1 | 5 ms | 60 ms | 4–6 dB GR |
| Mix BUS | Fruity Compressor | 1.5:1 | 30 ms | auto | 1–2 dB GR (glue) |

## 4. Time-Based FX (sends)
| Send | Plugin | Setting | Used by |
|---|---|---|---|
| MX75 Reverb plate | Fruity Reeverb 2 | decay 1.8s, pre-delay 20ms, EQ HPF 250 Hz LPF 8 kHz | snare, lead, hook |
| MX76 Delay 1/8 dot | Fruity Delay 3 | feedback 30%, ping-pong, HPF 400 Hz | lead, hook |
| Hall (Bridge only) | ValhallaSupermassive | — | pad in Bridge |

## 5. Stereo Image
- Mono < 120 Hz (utility plugin).
- Hat / shaker hard L/R alternating.
- Pad widest (M/S +130%).
- Lead center, octave-up layer wide.

## 6. Automation Final
- Vocal/Lead delay throw 1 bar after each phrase end (last 4 phrases of Drop2).
- Master volume +1 dB into Drop2.
- Reverb size automation in Bridge (+30%).

## 7. Reference Comparison (use ReaEQ + Spectrum)
| Metric | Reference | Mine | Action |
|---|---|---|---|
| Low energy 60–120 Hz | -8 dB | -5 dB | reduce sub bass -2 dB |
| Mid clarity 1–3 kHz | -12 dB | -16 dB | boost lead 1.5k +1.5 dB |
| Top air 10–14 kHz | -18 dB | -24 dB | high shelf master +2 dB (di mastering) |

## 8. A/B Test Pass
- [ ] Laptop speaker — bass terdengar sebagai hint, vocal jelas.
- [ ] Headphone — stereo balanced, no ear fatigue.
- [ ] Mobile phone — hook tetap kuat tanpa low end.
- [ ] Mono fold-down — tidak ada elemen hilang.

## 9. Bounce
- File: `bounces/v0.3.0-mix.wav` (24-bit / 48 kHz, peak -6 dBFS).
```
