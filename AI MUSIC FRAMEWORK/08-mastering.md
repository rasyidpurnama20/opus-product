# Stage 08 — Mastering → Master Notes

**Code:** `MST` | **Output:** `MMN-<track>-001`

## Purpose
Mengangkat mix sampai loudness & tonal balance kompetitif untuk platform target (Spotify, Apple Music, YouTube, broadcast) tanpa merusak dinamika.

## DoR
- [ ] Mix Notes `APPROVED` & bounce `v0.3.0-mix.wav` (peak -6 dBFS) ada.
- [ ] Sudah dengar di minimal 3 sistem berbeda dan revisi mix kalau perlu.

## DoD
- [ ] Master Notes memuat: target LUFS-I, true peak, plugin chain, frequency adjust, stereo width final, dither plan.
- [ ] 3 versi master: streaming (-14 LUFS), club/loud (-9 LUFS), broadcast (-23 LUFS atau target sesuai).
- [ ] LUFS terukur (bukan asumsi).

---

## Prompt Template

```
1. ROLE
You are a mastering engineer who respects the mix and only does what's necessary.

2. CONTEXT
Track ini akan rilis di: {{Spotify / SoundCloud / club DJ pool / sync ke video}}.

3. INPUT
- MN-{{slug}}-001: {{paste}}
- v0.3.0-mix.wav metering screenshot/desc: {{peak, RMS, LUFS short term avg}}.
- Reference master metering: {{Artist - Track loudness}}.

4. TASK
- Tetapkan target LUFS-I per platform.
- Sarankan mastering chain (urutan plugin) + setting konservatif.
- Tetapkan true-peak ceiling.
- Tetapkan stereo width tweak (jika perlu).
- Plan dither bila bouncing ke 16-bit.

5. OUTPUT
08-master-notes.md.

6. CONSTRAINTS
- Loudness war prevention: jangan smash > -8 LUFS-I kecuali target eksplisit.
- True peak ≤ -1 dBTP untuk streaming.
- Tidak boleh re-EQ besar (>3 dB). Kalau perlu, kembali ke mixing.

7. ACCEPTANCE
- [ ] Target LUFS-I per platform jelas.
- [ ] True-peak ceiling spesifik.
- [ ] Plugin chain ≤ 6 stages.
```

---

## Artifact Template — `MMN-<track>-001`

```markdown
# Master Notes — {{Track Title}}

| Field | Value |
|---|---|
| ID | MMN-{{slug}}-001 |
| Status | DRAFT |
| Linked MN | MN-{{slug}}-001 |
| Mix bounce | v0.3.0-mix.wav (peak -6 dBFS) |

## 1. Targets
| Platform | LUFS-I | True Peak | Format |
|---|---|---|---|
| Spotify / Apple / Tidal | -14 | -1 dBTP | 16/44.1 |
| Club / DJ pool | -9 to -10 | -0.3 dBTP | 24/48 |
| YouTube | -14 | -1 dBTP | 24/48 |
| Broadcast (PSA, podcast) | -23 | -2 dBTP | 24/48 |

## 2. Mastering Chain
1. **Subtractive EQ** (Fabfilter Pro-Q 3 / Fruity Parametric EQ 2)
   - Cut 200 Hz Q 1.5 -1 dB (residual mud).
   - Cut 3.2 kHz Q 2.0 -0.8 dB (harshness).
   - High shelf 12 kHz +1.5 dB (air).
2. **Tonal balancer / saturator** (Soundgoodizer / Fruity Soft Clipper)
   - Mode A, drive low, just for harmonic glue.
3. **Multiband compression** (Maximus, 3 bands)
   - Low: 1.5 dB GR.
   - Mid: 1 dB GR.
   - High: 0.5 dB GR.
4. **Stereo imager** (Fruity Stereo Shaper)
   - Mono below 120 Hz.
   - Width: low band 80%, mid 100%, high 110%.
5. **Final limiter** (Fruity Limiter / Pro-L 2)
   - Streaming version: ceiling -1 dBTP, target -14 LUFS-I.
   - Loud version: ceiling -0.3 dBTP, target -9 LUFS-I.
6. **Dither** (only when exporting 16-bit) — TPDF.

## 3. Reference Loudness Match
| Metric | Reference | Mine v0.3.0 mix | After mastering target |
|---|---|---|---|
| LUFS-I | -10 | -16 | -14 (stream) / -9 (loud) |
| True peak | -0.6 dBTP | -6 dBFS | -1 dBTP |
| LRA (loudness range) | 6 LU | 9 LU | 6–7 LU |
| Crest factor | 11 dB | 14 dB | 11–12 dB |

## 4. Tonal Tilt Check
Pakai tonal balance reference (Youlean / SPAN). Catat deviasi dari target curve & koreksi via EQ stage 1.

## 5. Bounce Plan
| Version | Sample rate | Bit | Naming |
|---|---|---|---|
| Streaming | 44.1 kHz | 24-bit + dither to 16 | `<slug>-v1.0.0-stream.wav` |
| Loud | 48 kHz | 24-bit | `<slug>-v1.0.0-loud.wav` |
| Broadcast | 48 kHz | 24-bit | `<slug>-v1.0.0-broadcast.wav` |
| Stems master | 48 kHz | 24-bit | `stems/v1.0.0/` |

## 6. Final A/B
- [ ] LUFS terukur match target (Youlean Loudness Meter).
- [ ] True peak terukur ≤ ceiling.
- [ ] Translate test: laptop, hp, mobil (bila bisa), headphone.
- [ ] Compare side-by-side dengan reference (volume matched).

## 7. Sign-off
Approved by {{nama}} on {{date}}.
```
