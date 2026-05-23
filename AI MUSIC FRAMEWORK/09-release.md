# Stage 09 — Release → Release Plan

**Code:** `REL` | **Output:** `RP-<track>-001`

## Purpose
Memastikan track yang sudah jadi sampai ke pendengar dengan packaging, metadata, dan timing yang benar.

## DoR
- [ ] Master Notes `APPROVED` & semua versi master tersedia.

## DoD
- [ ] Release Plan memuat: title final, artist credit, ISRC, metadata lengkap, distribusi, cover art brief, lyric (bila ada), sync clearance, marketing rollout.
- [ ] Cover art final.
- [ ] Distribusi terjadwal.

---

## Prompt Template

```
1. ROLE
You are a release manager / artist manager who handles music distribution end-to-end.

2. CONTEXT
Saya akan rilis track ini sebagai {{single / single dari EP / sync placement}}. Distributor saya: {{DistroKid / TuneCore / Ditto / label X}}. Audience target: {{deskripsi singkat}}.

3. INPUT
- MMN-{{slug}}-001: {{paste targets & versions}}.
- TB log line: {{...}}
- MB mood adjektif: {{...}}.

4. TASK
- Saran 5 alternatif title (bila belum final).
- Metadata lengkap: artist, featured, genre primer + sekunder, mood tag, BPM, key, ISRC placeholder.
- Cover art brief: konsep, palet warna, tipografi, do/don't.
- Lyric / songwriter credit (bila ada).
- Rollout timeline (D-21 sampai D+30).
- Distribusi platform list + target playlist pitch.

5. OUTPUT
09-release-plan.md.

6. CONSTRAINTS
- Genre tag harus dari taxonomy distributor (mis. Spotify genres).
- ISRC mengikuti format internasional.

7. ACCEPTANCE
- [ ] Title final dipilih.
- [ ] Cover art brief actionable untuk designer.
- [ ] Rollout timeline 30 hari.
```

---

## Artifact Template — `RP-<track>-001`

```markdown
# Release Plan — {{Track Title}}

| Field | Value |
|---|---|
| ID | RP-{{slug}}-001 |
| Status | DRAFT |
| Linked MMN | MMN-{{slug}}-001 |
| Release date | {{YYYY-MM-DD}} |

## 1. Identity
| Field | Value |
|---|---|
| Title | {{Final Title}} |
| Artist | {{Artist Name}} |
| Featured | {{...}} |
| Songwriter | {{credit}} |
| Producer | {{credit}} |
| Mixed by | {{credit}} |
| Mastered by | {{credit}} |
| Genre primary | Lo-fi Hip Hop |
| Genre secondary | Chillhop |
| Mood tags | nostalgic, late-night, warm |
| BPM | 92 |
| Key | F minor |
| Duration | 3:08 |
| ISRC | {{ID-XXX-26-NNNNN}} |
| UPC | {{from distributor}} |
| Explicit | No |
| Language | Instrumental |

## 2. Cover Art Brief
- **Concept:** night drive through suburban Jakarta in the rain, soft neon reflection.
- **Palette:** desaturated teal + warm amber.
- **Typography:** sans-serif modern, lowercase, lower-third placement.
- **Format:** 3000 × 3000 px, sRGB, JPG.
- **Variants:** square (cover), 9:16 (Reels/Story), 16:9 (YouTube).
- **Do:** keep face / text away from corners.
- **Don't:** logos pihak ketiga, foto orang tanpa release.

## 3. Distribution
| Platform | Status | Pitch playlist |
|---|---|---|
| Spotify | yes | "Lo-Fi Beats", "Chill Vibes" — pitch 14 hari sebelum |
| Apple Music | yes | "Pure Focus" |
| YouTube Music + topic channel | yes | — |
| SoundCloud | yes (preview) | — |
| TikTok / Reels | yes (15s + 60s edits) | — |
| Bandcamp | optional | — |

## 4. Edits
| Edit | Length | Use |
|---|---|---|
| Full | 3:08 | streaming |
| Radio | 2:30 | broadcast / sync |
| TikTok 1 | 0:15 | hook moment |
| TikTok 2 | 0:60 | drop |
| Looped 1h | 60:00 | study mix YouTube |

## 5. Rollout Timeline
| Day | Action |
|---|---|
| D-21 | Upload ke distributor, lock metadata |
| D-14 | Spotify for Artists pitch |
| D-10 | Cover art + 5 teaser snippet (Story/Reels) |
| D-7 | Pre-save link di bio, 3 short content |
| D-3 | Behind-the-scenes (FL Studio screenshot) |
| D-1 | Final reminder post |
| **D-0** | **Release**, post drop di semua channel |
| D+1..7 | Daily story (lirik visual / clip studio) |
| D+14 | Acoustic / alternate version teaser |
| D+30 | Numbers retro (next stage 09 retro) |

## 6. Sync / Licensing
- Available for sync: yes / no.
- Stems delivered to: {{library X / sync agency Y}}.
- Splits: {{nama : %}}, total 100%.
- Publisher: {{...}}.

## 7. Backups & Archive
- Project FLP final: `archive/<slug>-v1.0.0.flp`.
- All stems: `archive/<slug>-v1.0.0/stems/`.
- Master files: `archive/<slug>-v1.0.0/masters/`.
- Lyric / chord chart PDF: `archive/<slug>-v1.0.0/sheet.pdf`.
- README artist statement (untuk arsip personal): 200 kata.

## 8. Post-Release Retro (filled D+30)
- Streams: {{...}}
- Save rate: {{...}}
- Best-performing platform: {{...}}
- Lessons learned: {{...}}
```
