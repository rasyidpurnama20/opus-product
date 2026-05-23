# Stage 01 — Symptom Capture → Bug Report

**Code:** `SC` | **Output:** `BR-<bug-slug>-001`

## Purpose
Tangkap apa yang user/observer benar-benar lihat, bukan asumsi penyebab.

## DoD
- [ ] BR memuat: gejala (apa yang user lihat), env (versi, OS, browser, config), expected vs actual, frekuensi, severity, log/screenshot.

## Prompt
```
ROLE: SRE/QA yang bertanya tepat sebelum panic.
INPUT: laporan bug mentah (user/log/observasi).
TASK:
- Pisahkan gejala (apa yang dilihat) vs interpretasi (apa yang user kira).
- Tanya/cari: env, versi, browser/OS, config, waktu kejadian, frekuensi, dampak.
- Klasifikasi severity (critical/high/med/low).
- Tag area kode kemungkinan (best guess, bukan fix).
OUTPUT: 01-bug-report.md.
CONSTRAINTS: tidak boleh menyimpulkan root cause di stage ini.
ACCEPTANCE: gejala vs interpretasi dipisah, env lengkap, severity di-set.
```

## Template
```markdown
# Bug Report — {{title}}

| Field | Value |
|---|---|
| ID | BR-{{slug}}-001 |
| Severity | critical / high / medium / low |
| First seen | {{date/time + zone}} |
| Reporter | {{...}} |

## Symptom (what user sees)
{{Plain language: "App crashes when I click Save after editing avatar."}}

## NOT the symptom (interpretation to ignore for now)
- ~~"It's the auth service"~~ — no evidence yet.

## Environment
| Field | Value |
|---|---|
| App version | v3.4.1 |
| OS | macOS 14.5 |
| Browser | Chrome 124 |
| User config | premium tier, MFA enabled |
| Time | 2026-05-22 14:30 WIB |
| Region | ap-southeast-1 |

## Expected vs Actual
- **Expected:** Save button → "Saved" toast.
- **Actual:** White screen, console error `TypeError: Cannot read properties of undefined`.

## Frequency
- Reproducible: {{always / often / sometimes / once}}.
- Affected users: {{1 / cohort / all}}.

## Logs / Screenshots
- Console: {{paste / link}}.
- Server log: {{paste / link}}.
- Screenshot: {{...}}.

## Possible Areas (best guess only)
- Avatar upload pipeline.
- Save controller.
```
