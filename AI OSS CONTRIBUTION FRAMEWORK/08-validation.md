# Stage 08 — Validation → Validation Report

**Code:** `VL` | **Output:** `VR-<repo>-<issue#>`

## Purpose
Sebelum buka PR, **buktikan** ke diri sendiri (dan pre-empty ke reviewer) bahwa perubahan benar-benar bekerja & tidak break apa-apa.

## DoR
- [ ] Implementation selesai, branch siap.

## DoD
- [ ] Validation Report memuat: test result, lint/format/typecheck, manual smoke test, perf check (kalau hot path), backward compat check, security check.
- [ ] Semua hijau / ada catatan eksplisit untuk yang kuning.

---

## Prompt Template

```
1. ROLE
You are a release manager validating a patch.

2. CONTEXT
Saya selesai coding. Sebelum PR, saya butuh validation pass.

3. INPUT
- CP-{{repo}}-{{issue#}}: {{paste section "test plan" dan "out of scope"}}
- Output `pnpm test`, `pnpm lint`, `pnpm typecheck` saya: {{paste}}

4. TASK
- Cek output test: pass count, ada flaky?
- Cek lint, format, typecheck.
- Sarankan smoke test manual (mis. command + expected output).
- Backward compat: cari API public yang mungkin terdampak.
- Perf check: kalau hot path, sarankan benchmark mini.

5. OUTPUT
08-validation-{{issue#}}.md.

6. CONSTRAINTS
- Tidak boleh "skip karena ribet". Catat sebagai known limitation kalau perlu.

7. ACCEPTANCE
- [ ] Semua kategori dijawab (pass / fail / N/A + note).
```

---

## Artifact Template — `VR-<repo>-<issue#>`

```markdown
# Validation Report — {{owner/repo}}#{{issue#}}

| Field | Value |
|---|---|
| ID | VR-{{repo-slug}}-{{issue#}} |
| Branch | {{me/123-fix}} |
| Base | main @ {{sha}} |

## 1. Automated Checks
| Check | Command | Result |
|---|---|---|
| Tests | `pnpm test --run` | 415 passed, 0 failed (+3 new) |
| Lint | `pnpm lint` | 0 errors |
| Format | `pnpm format:check` | clean |
| Typecheck | `pnpm typecheck` | clean |
| Build | `pnpm build` | success |

## 2. New Test Cases Added
| Test | What it covers |
|---|---|
| `validate.test.ts > maps Zod to 422` | regression for #123 |
| `validate.test.ts > propagates non-validation error` | side-effect protection |
| `validate.test.ts > no info leak in 422 body` | security |

## 3. Manual Smoke
```bash
pnpm dev
curl -X POST http://localhost:3000/api/users \
  -H 'Content-Type: application/json' \
  -d '{"email":"x"}'
# Expected: 422 {"code":"VALIDATION_ERROR","field":"email"}
# Got:      ✅ exact match
```

## 4. Backward Compatibility
- Public API touched: NO (middleware internal).
- Type exports changed: 1 added, none changed/removed.
- Migration needed: NO.

## 5. Performance Check
- Hot path? NO (validator runs per request, but already throws — no extra work).
- Benchmark: N/A.

## 6. Security Considerations
- Error body sanitized (no stack trace, no internal path).
- No new dependency.
- No sensitive logging added.

## 7. Cross-Platform / Multi-Env
- Linux: ✅
- macOS: ✅
- Windows: not tested (note in PR).

## 8. Open Risks
- Some controllers might rely on 500 to trigger retry middleware — flagged in PR description, asking maintainer.

## 9. Verdict
**READY FOR PR**.
```
