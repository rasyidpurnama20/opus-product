# Stage 05 — Reproduction → Repro Report

**Code:** `RP` | **Output:** `RR-<repo>-<issue#>`

## Purpose
**Untuk bug:** mereproduksi masalah secara konsisten sebelum mencoba fix. **Untuk feature:** menulis "before state" — perilaku saat ini & gap.

> Stage ini boleh di-skip untuk perubahan trivial (typo, doc fix). Tapi *tidak* untuk bug atau feature.

## DoR
- [ ] Setup Log selesai, environment hijau.

## DoD
- [ ] Repro Report memuat: minimal repro steps, expected vs actual, scope (apakah hanya di config X?), commit yang memperkenalkan (kalau ketemu via git bisect), dampak.

---

## Prompt Template

```
1. ROLE
You are a senior QA + bisecter who finds the smallest reliable repro.

2. CONTEXT
Saya akan mengerjakan {{issue#}}. Sebelum coding, saya butuh konfirmasi behavior current.

3. INPUT
- Issue body: {{paste}}
- Repro yang user laporkan: {{paste}}
- Versi yang terdampak menurut user: {{...}}.

4. TASK
- Tulis ulang minimal repro (paling singkat yang masih reliable).
- Jalankan & catat: expected vs actual.
- Cek apakah hanya terjadi di OS / env / config tertentu.
- Coba git bisect kalau ada commit hash sebelum & sesudah bug.
- Estimasi dampak: berapa user, severity, ada workaround?

5. OUTPUT
05-repro-report-{{issue#}}.md.

6. CONSTRAINTS
- Repro harus deterministik (atau jelaskan flakiness-nya).
- Belum boleh menulis fix.

7. ACCEPTANCE
- [ ] Repro reproducible 3 kali berturut-turut.
- [ ] Expected vs actual jelas.
- [ ] Scope (mana terjadi, mana tidak) jelas.
```

---

## Artifact Template — `RR-<repo>-<issue#>`

```markdown
# Repro Report — {{owner/repo}}#{{issue#}}

| Field | Value |
|---|---|
| ID | RR-{{repo-slug}}-{{issue#}} |
| Reproduced | YES / PARTIAL / NO |
| Status | DRAFT |
| Linked IB | IB-{{repo-slug}}-{{issue#}} |

## 1. Minimal Repro
```bash
# from clean clone, on commit <sha>
pnpm install
pnpm dev
# in another terminal
curl -X POST http://localhost:3000/api/users \
  -H 'Content-Type: application/json' \
  -d '{"email": "x"}'
```

## 2. Expected vs Actual
- **Expected:** 422 with `{ "code": "INVALID_EMAIL" }`.
- **Actual:** 500 with stack trace leaking internal path.

## 3. Reliability
- Reproduced **3/3** runs.
- Flaky? NO.

## 4. Scope
| Variable | Value(s) reproduced | Value(s) not reproduced |
|---|---|---|
| Node | 18, 20 | 22 |
| OS | macOS, Ubuntu | Windows (not tested) |
| `config.strict` | true | false |
| Commit | from `v3.4.0` onwards | `v3.3.x` clean |

## 5. Bisect (optional)
```bash
git bisect start
git bisect bad v3.4.0
git bisect good v3.3.5
# → bisect lands on commit a1b2c3d
```
- First bad commit: `a1b2c3d "validate users middleware"`.

## 6. Impact
- Severity: **High** (5xx leaking internal info).
- Affected users: anyone with `config.strict = true` (default in v3.4+).
- Workaround: set `config.strict = false`.

## 7. Hypothesis (one-liner)
{{Validator melempar uncaught error karena tidak ada try-catch di `users.controller.ts:45`.}}
```
