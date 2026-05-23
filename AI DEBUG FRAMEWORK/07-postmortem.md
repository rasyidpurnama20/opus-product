# Stage 07 — Postmortem (incidents only)

**Code:** `PM` | **Output:** `PM-<bug-slug>-001`

## Purpose
Untuk insiden produksi (severity high/critical): dokumentasi blameless yang bisa dishare ke tim/stakeholder, supaya pembelajaran nyebar.

## DoD
- [ ] Postmortem: TL;DR, dampak (user impact, downtime, revenue), timeline detail, RCA ringkas, what went well, what went poorly, action items dengan owner & due date.

## Prompt
```
ROLE: postmortem writer (blameless culture).
INPUT: BR + IL + RCA + FX.
TASK:
- TL;DR 2 kalimat (untuk eksekutif).
- Dampak: kuantifikasi (X user terdampak, Y menit, $Z).
- Timeline detail: detection, escalation, mitigation, resolution.
- What went well (≥ 3): respons cepat, monitoring catch, dst.
- What went poorly (≥ 3): gap deteksi, dst.
- Action items: blameless, ownership eksplisit, due date.
OUTPUT: 07-postmortem.md.
CONSTRAINTS: bahasa netral, tidak menyalahkan individu.
ACCEPTANCE: dampak dikuantifikasi, ≥ 3 win + ≥ 3 loss, ≥ 3 action items dengan owner+date.
```

## Template
```markdown
# Postmortem — {{title}}

| Field | Value |
|---|---|
| ID | PM-{{slug}}-001 |
| Severity | SEV-2 (high) |
| Date | {{...}} |
| Status | Resolved |

## TL;DR
> Selama 6 jam pada {{date}}, sebagian user (premium tier) tidak bisa menyimpan avatar > 5MB. Penyebab: CDN response_body_limit tidak diupdate ketika avatar API berubah ke embedded base64 (PR #421). Diatasi dengan menaikkan limit; follow-up untuk reverse API ke URL-based.

## Impact
| Metric | Value |
|---|---|
| Users affected | ~1,200 (8% of premium) |
| Duration | 6h 12m |
| SLA breach? | yes (uptime 99.5% commitment) |
| Estimated revenue impact | ~$X |
| Support tickets | 47 |

## Timeline
| Time | Event |
|---|---|
| 00:00 | PR #421 deployed (avatar API change) |
| 00:42 | First user report on Twitter |
| 01:15 | Support escalation to engineering |
| 02:30 | Repro confirmed |
| 04:10 | Root cause: CDN limit |
| 05:30 | Fix deployed (limit raise to 10MB) |
| 06:12 | All affected users confirmed working |

## RCA Summary
{{1 paragraf — singkat dari RCA-{{slug}}-001.}}

## What Went Well
- Repro reproduced quickly (under 2.5h from first report).
- Status page updated proactively.
- CDN config change rolled forward safely (canary 10% then 100%).

## What Went Poorly
- No proactive monitoring for CDN truncation.
- Cross-team API contract review missing.
- Internal status communication slow (first internal alert 1h after first user report).

## Action Items
| # | Action | Owner | Due | Status |
|---|---|---|---|---|
| AI-1 | Add alert: CDN truncated responses > N/min | infra | 2 weeks | open |
| AI-2 | Reverse avatar API to URL-based | platform | 4 weeks | open |
| AI-3 | "API contract change" checklist incl. CDN config | dev experience | 3 weeks | open |
| AI-4 | Audit endpoints with response > 1MB | platform | 2 weeks | open |
| AI-5 | Add internal Slack alert when status page updated | infra | 1 week | open |

## Lessons
- Hardening config (security limits) must be paired with monitoring of when they are hit.
- Cross-team config dependencies need explicit handshake.

## Sign-off
- Incident commander: {{name}}.
- Reviewers: {{names}}.
- Date: {{...}}.
```
