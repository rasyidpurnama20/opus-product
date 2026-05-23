# Stage 09 — Pull Request → PR Submission

**Code:** `PR` | **Output:** `PRS-<repo>-<issue#>`

## Purpose
Membuka PR dengan title + body yang **memudahkan reviewer bilang "yes"**: konteks lengkap, alasan pilihan jelas, bukti validasi, screenshot bila perlu.

## DoR
- [ ] Validation Report `READY FOR PR`.

## DoD
- [ ] PR title mengikuti convention repo.
- [ ] PR body memuat: link issue, ringkasan, alternatives, test plan, validation, breaking-change note (kalau ada), screenshots (kalau UI).
- [ ] Self-review pass.

---

## Prompt Template

```
1. ROLE
You are a maintainer-friendly contributor. You write PR descriptions reviewers thank you for.

2. CONTEXT
Saya akan submit PR.

3. INPUT
- CP, VR, RR untuk issue ini.
- Style PR repo (isi PULL_REQUEST_TEMPLATE.md):
{{paste}}

4. TASK
- Susun title (concise, conventional).
- Susun body mengikuti template repo.
- Highlight breaking change kalau ada.
- Tambahkan "Considered alternatives" supaya reviewer tahu sudah dipikir.
- Sertakan checklist (test, docs, changelog).

5. OUTPUT
09-pr-submission-{{issue#}}.md (preview body sebelum submit).

6. CONSTRAINTS
- Title ≤ 70 char.
- Body to-the-point, hindari dramatis.
- Sertakan link issue dengan kata "Fixes #N" / "Closes #N" kalau memang menutup.

7. ACCEPTANCE
- [ ] Title & body lulus PR template repo.
- [ ] Link issue tertulis.
- [ ] Test plan ada.
```

---

## Artifact Template — `PRS-<repo>-<issue#>`

```markdown
# PR Submission — {{owner/repo}}#{{issue#}}

| Field | Value |
|---|---|
| ID | PRS-{{repo-slug}}-{{issue#}} |
| PR URL | (filled after submit) |
| Branch | me/123-fix-validate |
| Target | main |

## Title
`fix(validate): map validator throws to 422 instead of 500 (#123)`

## Body
```markdown
### Summary
Validator errors (Zod/Joi throws) bubbled up as 500 with stack trace.
This PR catches them in the validate middleware and returns 422 with
a sanitized payload.

Fixes #123.

### Approach
Localized fix in `src/middleware/validate.ts` (single try/catch + error mapper).
Considered:
- (B) Controller-level catch — smaller diff but doesn't address root cause.
- (C) Global error handler — too broad, separate PR (will open if maintainers want).

### Test Plan
- New unit tests in `validate.test.ts`:
  - Zod throw → 422.
  - Non-validation runtime error → still 500.
  - 422 body sanitized (no schema leakage).
- All existing tests still pass (`pnpm test` = 415 passed).

### Validation
- Lint, format, typecheck: clean.
- Manual smoke: `curl POST /api/users {email:"x"}` → 422.
- Built locally: success.

### Breaking Change
None expected — but if any caller relies on 500 from validator (e.g., retry middleware), they'll see 422 now. Flagging for review.

### Out of Scope
- Sanitization for non-validation 5xx → separate PR.
- Refactor controllers to global error handler → separate PR.

### Checklist
- [x] Linked issue
- [x] Tests added
- [x] Docs updated (CHANGELOG.md)
- [x] Self-review done
```

## Pre-Submit Self-Review
- [ ] Membaca diff sendiri dari awal sampai akhir.
- [ ] Komentar lama / println dibuang.
- [ ] PR ≤ 400 LOC kalau bukan refactor masif.
- [ ] Title cocok dengan first commit.
- [ ] Branch up-to-date dengan main (rebase atau merge sesuai house style).

## Post-Submit Action
- Cek CI hijau dalam 30 menit.
- Tag maintainer kalau ada blocker dependency.
- Jangan push lagi sampai ada review (kecuali fix CI).
```
