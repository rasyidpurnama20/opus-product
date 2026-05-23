# Stage 06 — Fix → Fix + Regression Test

**Code:** `FX` | **Output:** code commit + `FX-<bug-slug>-001` (fix log)

## Purpose
Fix yang **menargetkan root cause**, plus regression test supaya tidak balik lagi.

## DoD
- [ ] Fix patch + regression test merged.
- [ ] Re-run repro: gone.
- [ ] Fix log: alternatif yang dipertimbangkan, mengapa pilih ini, follow-up actions.

## Prompt
```
ROLE: senior engineer yang fix problem dengan diff terkecil.
INPUT: RCA + repo akses.
TASK:
- 2–3 alternatif fix dengan trade-off.
- Pilih satu, diff sekecil mungkin.
- Tulis regression test yang FAIL tanpa fix dan PASS dengan fix.
- Identifikasi follow-up (yang bukan scope fix langsung tapi perlu).
OUTPUT: 06-fix-log.md + diff.
CONSTRAINTS: target root cause, bukan sekadar hide symptom.
ACCEPTANCE: regression test ada, repro hilang, alternatif terdokumentasi.
```

## Template
```markdown
# Fix Log — {{title}}

| Field | Value |
|---|---|
| ID | FX-{{slug}}-001 |
| Linked RCA | RCA-{{slug}}-001 |
| PR | {{...}} |

## Alternatives
- A: Naikkan CDN limit ke 10MB. Fast, but masks root issue.
- B: Revert avatar API ke URL+lazy fetch. Solve root, ~2 day work.
- **C: Naikkan limit ke 10MB sebagai immediate, lalu plan A→B di sprint berikut.** ← chosen
- D: Add response compression. Complementary, separate PR.

## Chosen Approach
C: 2-step.
- **Step 1 (immediate):** raise CDN `response_body_limit` to 10MB. Patch commit.
- **Step 2 (planned):** reverse avatar API to URL-based with lazy fetch (separate ticket).

## Regression Tests
- **Integration:** call `/api/avatar/save` with 6MB avatar, assert response complete and JSON.parse succeeds.
- **CDN config drift test:** `response_body_limit` minimum 10MB asserted in IaC test.

## Re-Run Repro
- Before fix: crash 3/3.
- After fix: success 5/5.

## Follow-Up Actions
- Ticket A: revert avatar API ke URL-based (target sprint 23).
- Ticket B: alert when CDN truncates response.
- Ticket C: add cross-team review checklist for API contract changes.
- Ticket D: audit endpoint lain > 1MB.

## Communication
- Status update di channel #incidents.
- Notify reporter user (kalau eksternal).
```
