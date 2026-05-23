# Stage 04 — Investigation → Investigation Log

**Code:** `IV` | **Output:** `IL-<bug-slug>-001`

## Purpose
Mengumpulkan bukti & menggugurkan/mengkonfirmasi hipotesis dengan disiplin.

## DoD
- [ ] Setiap hipotesis di HL punya status: confirmed / refuted / inconclusive.
- [ ] Kalau ada hipotesis baru muncul, ditambahkan + diuji.
- [ ] Bukti tertulis (log snippet, screenshot, perintah).

## Prompt
```
ROLE: investigator metodis. Satu langkah satu hipotesis.
INPUT: HL + akses log/repo.
TASK:
- Per hipotesis terurut: jalankan test, catat hasil mentah, simpulkan confirmed/refuted.
- Kalau confirmed: lanjut narrowing (bisect, bin-search).
- Kalau semua refuted: stop & generate hipotesis baru bersama saya.
- Catat surprise findings (sering memberi clue baru).
OUTPUT: 04-investigation.md.
CONSTRAINTS: jangan lompat ke fix; investigation dulu.
ACCEPTANCE: tiap H di HL punya verdict, bukti tersaji.
```

## Template
```markdown
# Investigation Log — {{title}}

| Field | Value |
|---|---|
| ID | IL-{{slug}}-001 |
| Linked HL | HL-{{slug}}-001 |

## Investigation 1 — H2 (malformed JSON)
- **Test:** open DevTools Network, click Save with 5.5MB avatar.
- **Observation:** response 200, body **truncated** at 1 MB. JSON.parse throws.
- **Verdict:** **CONFIRMED**.
- **Evidence:**
  ```
  Content-Length: 5532019
  Actual received: 1048576
  ```

## Narrowing 1 — Where does truncation happen?
- Test A: bypass CDN with `--resolve` → full body received.
- Test B: through CDN → truncated at 1 MB.
- **Verdict:** truncation at CDN layer.

## Narrowing 2 — Why CDN truncates at 1 MB?
- Check CDN config: `response_body_limit: 1MB` set 6 months ago for "security".
- This was OK when avatar API returned URLs only. After v3.4.0, API began returning embedded base64 blob, which can exceed 1 MB.

## Verdict per Hypothesis
| H | Status | Note |
|---|---|---|
| H1 | refuted | render fine when full body present |
| H2 | confirmed | truncated body → JSON.parse fail |
| H3 | confirmed (causal) | CDN response_body_limit |
| H4 | refuted | no OOM events |
| H5 | refuted | no race in single-user repro |

## Surprise Findings
- v3.4.0 changed avatar API behavior without updating CDN config.
- Other endpoints might also exceed 1 MB silently → wider audit needed.

## Next Step
→ Stage 05 RCA (root + 5 whys).
```
