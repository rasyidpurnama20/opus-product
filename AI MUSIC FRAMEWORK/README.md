# AI MUSIC FRAMEWORK

Framework prompt **berbasis artifact** untuk komposer & producer musik yang bekerja di **FL Studio** (atau DAW lain) bersama AI.

AI tidak (belum) bisa "menekan tombol" di FL Studio, tapi bisa jadi partner yang luar biasa untuk:
- Eksplorasi mood, referensi, genre.
- Saran progresi akor, scale, BPM, key, tempo modulation.
- Struktur arrangement & energy curve.
- Saran sound design (synth preset family, layering, processing).
- Mixing/mastering checklist sesuai genre.
- Metadata, cover brief, distribution.

## Prinsip
1. **Mood dulu, baru not.** Stage 01 melarang menulis melodi sebelum mood jelas.
2. **Bar-accurate arrangement sebelum sound design.** Hindari "tinggal nambah pad" yang bikin mix berantakan.
3. **Reference-driven.** Tiap pilihan creative perlu referensi konkret (track, plugin, preset).
4. **Mix bukan rescue.** Masalah arrangement tidak diselesaikan di mix.
5. **Versi setiap render.** Setiap bounce punya commit-id (v0.1.0, v0.2.0, dst).

## Stages

```
[01-Inspiration]  ──► Mood Board (MB)
       │
       ▼
[02-Concept]      ──► Track Brief (TB)
       │
       ▼
[03-Sketch]       ──► Melodic Sketch (MS)        ← MIDI sketch + chord chart
       │
       ▼
[04-Arrangement]  ──► Arrangement Map (AM)       ← bar-by-bar, energy curve
       │
       ▼
[05-Sound Design] ──► Sound Palette (SP)         ← instrument per section
       │
       ▼
[06-Production]   ──► Production Plan (PP)       ← FL Studio project structure
       │
       ▼
[07-Mixing]       ──► Mix Notes (MN)
       │
       ▼
[08-Mastering]    ──► Master Notes (MMN)
       │
       ▼
[09-Release]      ──► Release Plan (RP)
```

| # | Stage | Output | Code |
|---|---|---|---|
| 01 | Inspiration | Mood Board | `MB` |
| 02 | Concept | Track Brief | `TB` |
| 03 | Sketch | Melodic Sketch | `MS` |
| 04 | Arrangement | Arrangement Map | `AM` |
| 05 | Sound Design | Sound Palette | `SP` |
| 06 | Production | Production Plan | `PP` |
| 07 | Mixing | Mix Notes | `MN` |
| 08 | Mastering | Master Notes | `MMN` |
| 09 | Release | Release Plan | `RP` |

## Konvensi ID
`<CODE>-<track-slug>-<NNN>`. Contoh: `MB-summer-night-001`, `AM-summer-night-001`.

## Folder Layout untuk Project Anda
```
projects/<track-slug>/
├── 01-mood-board.md
├── 02-track-brief.md
├── 03-melodic-sketch.md
├── 04-arrangement-map.md
├── 05-sound-palette.md
├── 06-production-plan.md
├── 07-mix-notes.md
├── 08-master-notes.md
├── 09-release-plan.md
├── refs/                  ← MP3/link referensi
├── flp/                   ← project file FL Studio
├── stems/                 ← export stem per section
└── bounces/               ← versi render: v0.1.0.wav, v0.2.0.wav
```

## Anti-Pattern Umum
- Loncat ke "buka FL Studio dan main-main" tanpa mood board → 80% berakhir di folder unfinished.
- Mixing sebelum arrangement final → buang waktu.
- Tidak ada referensi → AI & telinga sendiri sama-sama nyasar.
- Mastering sebelum mix selesai.
- Tidak menyimpan versi bounce → tidak bisa A/B compare.
