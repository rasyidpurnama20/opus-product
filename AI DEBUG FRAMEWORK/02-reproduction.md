# Stage 02 — Reproduction → Repro Recipe

**Code:** `RP` | **Output:** `RR-<bug-slug>-001`

## Purpose
Punya langkah yang **selalu** menghasilkan bug. Tidak punya repro = tidak siap fix.

## DoD
- [ ] Repro yang reproducible 3/3 kali.
- [ ] Lingkungan minimal (data, config, env yang strictly necessary).

## Prompt
```
ROLE: bisecter / minimizer yang sabar.
INPUT: BR-{{slug}}-001.
TASK:
- Coba reproduksi step-by-step.
- Kurangi jadi minimal repro: variabel mana yang HARUS ada.
- Catat 3× run dengan cap reliability (3/3? flaky?).
- Identifikasi boundary (kapan terjadi, kapan tidak).
OUTPUT: 02-repro-recipe.md.
CONSTRAINTS: tidak boleh fix dulu.
ACCEPTANCE: minimal repro + 3 run hasil.
```

## Template
```markdown
# Repro Recipe — {{title}}

| Field | Value |
|---|---|
| ID | RR-{{slug}}-001 |
| Reproducibility | 3/3 |
| Linked BR | BR-{{slug}}-001 |

## Minimal Repro
```bash
# 1. seed user with avatar > 5 MB
# 2. login
# 3. open profile
# 4. click "Save" (without changing anything)
# 5. observe white screen + console error
```

## Variables
| Variable | Value reproduces | Value does NOT reproduce |
|---|---|---|
| Avatar size | > 5 MB | ≤ 5 MB |
| Browser | Chrome, FF | Safari (different error) |
| Network | online | offline (different error) |
| Tier | premium / free | (same) |

## Run Log
- Run 1: white screen ✅
- Run 2: white screen ✅
- Run 3: white screen ✅

## Boundary
- Threshold appears at avatar size ~5.0 MB. At 4.9 MB, save succeeds. At 5.1 MB, fails.

## Hypothesis Seed (for stage 03)
- Looks size-related → upload payload limit? or rendering of returned blob?
```
