# Stage 06 — Publish → Publish Plan

**Code:** `PB` | **Output:** `PB-<piece-slug>-001`

## Purpose
Distribusi: bukan upload-and-pray, tapi rencana yang menjangkau audience target.

## DoD
- [ ] Publish plan: platform target, format conversion (markdown → platform), schedule, cross-post strategy, social media teaser.
- [ ] Pre-publish checklist tuntas.
- [ ] Post-publish: tracking + response plan.

## Prompt
```
ROLE: distribution / content strategist.
INPUT: AB + final piece + saya punya channel apa saja.
TASK:
- Tetapkan platform primary + cross-post.
- Conversion: tulisan saya butuh adjustment apa per platform (Medium, dev.to, LinkedIn, hashnode, personal blog)?
- Sketsa social teaser: 1 thread Twitter, 1 LinkedIn post, 1 IG carousel (kalau relevant).
- Saran timing publish (hari + jam) sesuai persona.
- Pre-publish + post-publish checklist.
OUTPUT: 06-publish-plan.md.
CONSTRAINTS: realistis dengan effort saya. Jangan over-cross-post.
ACCEPTANCE: primary + cross-post listed, teaser drafted, schedule, checklist.
```

## Template
```markdown
# Publish Plan — {{Piece Title}}

| Field | Value |
|---|---|
| ID | PB-{{slug}}-001 |
| Publish date | {{...}} |
| Primary platform | personal blog (own domain) |
| Cross-post | dev.to (canonical to blog), LinkedIn (excerpt) |

## Pre-Publish Checklist
- [ ] Final draft committed to repo / CMS.
- [ ] Headline final.
- [ ] Meta description.
- [ ] Cover image / og:image (1200×630).
- [ ] Author bio + photo.
- [ ] Tags (max 5).
- [ ] Category.
- [ ] Internal links to my other posts (≥ 1).
- [ ] External links open new tab (where intended).
- [ ] Schema.org Article markup (kalau personal blog).

## Conversion Per Platform
| Platform | Adjustment |
|---|---|
| Personal blog | full version, code snippets in proper highlight |
| dev.to | canonical URL ke personal blog; tags `python`, `async`, `concurrency` |
| LinkedIn | excerpt 800 char + link; tag relevant connections |
| Hashnode | (skip kalau effort > value) |

## Social Teasers

### Twitter / X (thread, 5 tweets)
1. "If your async Python code occasionally hangs and you can't tell why—it's probably leaked tasks. Here's the fix that took me 5 years to understand. 🧵"
2. "(...)" [paste 4 more]
5. "Full post: {{link}}. Try it on one hot path this week."

### LinkedIn
> [180 words excerpt + link, profesional tapi personal]

### Newsletter (kalau punya)
> Subject: "Task Groups: Mengapa async Python sering bocor"

## Schedule
| When | Action |
|---|---|
| D-1 evening | Final read; queue posts |
| D-0 09:00 WIB (Tue/Wed) | Publish primary |
| D-0 09:30 | Post Twitter thread |
| D-0 10:00 | Post LinkedIn |
| D-0 11:00 | Cross-post dev.to |
| D-0 evening | Reply ke comments |
| D+1 morning | Post 1 follow-up tweet (specific quote) |
| D+3 | Post 1 long-form summary di LinkedIn |
| D+7 | Reflection: numbers + lessons |

## Response Plan
- Comment di blog: respond dalam 24 jam.
- DM dengan pertanyaan teknis: respond ringkas, link ke resource bila perlu.
- Critical / disagreement: respond dengan rasa ingin tahu, jangan defensif.
- Spam: ignore / delete.

## Post-Publish Tracking (D+7)
- Pageviews: {{...}}
- Median read time: {{...}}
- Top referrer: {{...}}
- Comments / replies: {{...}}
- Lessons / next idea: {{...}}
```
