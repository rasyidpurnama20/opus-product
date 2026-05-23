# Stage 03 — Hypothesis → Hypothesis Log

**Code:** `HY` | **Output:** `HL-<bug-slug>-001`

## Purpose
Tulis daftar dugaan **sebelum** investigasi, supaya tidak bias kemana-mana saat baca log/code.

## DoD
- [ ] HL memuat: 3+ hipotesis, prior probabilitas (gut feel %), test plan untuk setiap hipotesis (mis. log apa yang dicek), urutan investigasi.

## Prompt
```
ROLE: detektif yang menulis daftar tersangka sebelum interogasi.
INPUT: BR + RR.
TASK:
- Generate 3–5 hipotesis sebab.
- Per hipotesis: prior (gut %), bukti yang akan menguatkan, bukti yang akan menggugurkan, cara test cepat (≤ 30 menit).
- Urutkan dari "termurah dipastikan" ke "termahal".
- Tulis "non-hypotheses" (yang sudah diverifikasi bukan): biar tidak diulang.
OUTPUT: 03-hypothesis.md.
ACCEPTANCE: 3+ hipotesis, prior, test plan, urutan.
```

## Template
```markdown
# Hypothesis Log — {{title}}

| Field | Value |
|---|---|
| ID | HL-{{slug}}-001 |
| Linked RR | RR-{{slug}}-001 |

## Hypotheses (ranked by cheap-to-test)

### H1 — Frontend rendering issue with returned base64 blob
- Prior: 40%
- Confirm if: removing `<img src={blob}>` render avoids crash.
- Refute if: same crash without rendering.
- Cheap test: comment out render, click Save → 5 min.

### H2 — Backend returns malformed JSON when avatar > 5 MB
- Prior: 30%
- Confirm if: response body invalid JSON.
- Cheap test: inspect Network tab → 5 min.

### H3 — CDN truncates large response body
- Prior: 15%
- Confirm if: direct call to origin (bypass CDN) succeeds.
- Cheap test: curl `--resolve` to origin → 10 min.

### H4 — Memory limit exhausted on backend pod
- Prior: 10%
- Confirm if: pod OOMKill in events log.
- Cheap test: kubectl describe pod → 5 min.

### H5 — Race condition with separate avatar service
- Prior: 5%
- Cheap test: enable trace logging, inspect → 30 min.

## Investigation Order
1. H2 (cheapest, evidence already partial)
2. H1
3. H4
4. H3
5. H5

## Non-Hypotheses (already ruled out)
- Auth issue: tested with fresh token, same crash.
- Browser cache: tested incognito.
```
