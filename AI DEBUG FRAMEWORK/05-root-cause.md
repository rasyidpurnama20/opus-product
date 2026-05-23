# Stage 05 — Root Cause → RCA Document

**Code:** `RC` | **Output:** `RCA-<bug-slug>-001`

## Purpose
Mendokumentasikan penyebab inti, bukan symptom. Pakai 5 Whys atau fishbone, supaya fix ditujukan ke akar.

## DoD
- [ ] RCA: timeline kronologis, 5-whys atau fishbone, kontributor (technical + process), bedakan trigger vs root cause, daftar contributing factor.

## Prompt
```
ROLE: incident commander pasca-investigasi.
INPUT: IL-{{slug}}-001 + history (commit yang relevan).
TASK:
- Susun timeline kronologis (kapan ditambahkan, kapan terdampak, kapan di-detect).
- Lakukan 5 whys.
- Bedakan: trigger (what made it happen now), proximate cause (immediate technical cause), root cause (underlying systemic).
- Identifikasi contributing factor (process, monitoring, dokumentasi).
OUTPUT: 05-rca.md.
CONSTRAINTS: blameless — fokus sistem, bukan orang.
ACCEPTANCE: 5 whys, trigger vs root vs contributing.
```

## Template
```markdown
# RCA — {{title}}

| Field | Value |
|---|---|
| ID | RCA-{{slug}}-001 |
| Linked IL | IL-{{slug}}-001 |
| Severity | high |

## Timeline
| Time | Event |
|---|---|
| 6 months ago | CDN config `response_body_limit: 1MB` added for DDoS hardening |
| 2 weeks ago | v3.4.0 changed avatar response from URL to embedded base64 blob (PR #421) |
| 3 days ago | First user report of white screen on save |
| 1 day ago | Triage assigned, repro confirmed |
| Today | RCA |

## 5 Whys
- Q1: Mengapa avatar save crash? → backend response truncated → JSON.parse fail.
- Q2: Mengapa response truncated? → CDN limit 1MB.
- Q3: Mengapa CDN limit 1MB melewati? → response body sekarang berisi base64 blob, dulu URL.
- Q4: Mengapa change ini lewat tanpa update CDN limit? → tidak ada checklist menghubungkan API change → CDN config.
- Q5: Mengapa tidak ada checklist? → CDN config dipegang tim infra terpisah; tidak ada "API contract change" review.

## Trigger vs Root Cause
- **Trigger:** PR #421 (kontent change avatar API).
- **Proximate cause:** CDN truncates response.
- **Root cause:** absence of cross-team review when API contract changes.

## Contributing Factors
- No alert when CDN truncates.
- No integration test that exercises >1MB response paths.
- API contract changelog tidak terkait CDN config repository.

## Blameless Note
Engineer di PR #421 tidak salah individu — sistem reviewnya yang punya gap. Fix harus pada sistem.
```
