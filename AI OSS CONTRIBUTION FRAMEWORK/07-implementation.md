# Stage 07 — Implementation → Patch

**Code:** `IM` | **Output:** Commits di branch kerja

## Purpose
Tulis kode mengikuti Change Plan, dalam gaya rumah, dengan commit message profesional.

## DoR
- [ ] Change Plan siap.

## DoD
- [ ] Semua file yang direncanakan tersentuh, file di luar plan **tidak**.
- [ ] Test ditambah / diubah sesuai plan.
- [ ] Lint + format + typecheck hijau.
- [ ] Commit message conventional, 1 commit = 1 langkah logis.

---

## Prompt Template

```
1. ROLE
You are a senior engineer pair-programming on someone else's repo.
You match the repo's style strictly.

2. CONTEXT
Saya implement perubahan ini.

3. INPUT
- CP-{{repo}}-{{issue#}}: {{paste}}
- File existing yang relevan: {{paste isi file pendek}}
- Coding style cues dari CM: {{paste}}

4. TASK
- Tulis diff per file sesuai Change Plan.
- Match style (naming, imports, docstring/JSDoc, error format).
- Tulis test sebelum / bersamaan dengan kode (TDD friendly).
- Buat commit message conventional, atomic per logical step.
- Hindari mengubah file di luar plan.

5. OUTPUT
- Diff (saya akan apply manual / paste sebagai patch).
- Commit message tiap commit.

6. CONSTRAINTS
- Tidak menambah dependency baru.
- Tidak refactor file yang tidak terkait.
- Komentar baru hanya kalau ada nilai (jangan over-comment).

7. ACCEPTANCE
- [ ] Diff hanya menyentuh file di Change Plan.
- [ ] Test lulus lokal.
- [ ] Lint + typecheck pass.
- [ ] Commit message conventional + atomic.
```

---

## House Style Quick-Reference (isi spesifik repo Anda)

```markdown
## House Style — {{owner/repo}}

| Aspect | Rule |
|---|---|
| File naming | kebab-case.ts |
| Type / interface | PascalCase |
| Function | camelCase |
| Constants | UPPER_SNAKE_CASE |
| Imports order | builtin → external → internal (eslint-plugin-import) |
| Error class | extends `RepoError` from `src/errors.ts` |
| Logger | `import { logger } from "@/logger"` |
| Async style | always async/await, no .then chains |
| Test file | colocated `*.test.ts` |
| Test framework | vitest, `describe/it` style |
| Mock | msw for HTTP, no jest.mock |
| Commit msg | conventional: `<type>(<scope>): <subject>` |
| Test required | yes for any non-trivial change |
```

---

## Commit Message Examples (gunakan ini sebagai cetakan)

```
fix(validate): catch validator throw and return 422

Previously, schema validation errors bubbled up as 500.
This wraps validator invocation in try/catch and maps
Zod/Joi errors to 422 with a sanitized payload.

Fixes #123.
```

```
test(validate): add failing tests for uncaught throw

Three cases:
- invalid email -> 422 not 500
- missing required field -> 422
- non-validation runtime error still propagates as 500
```

```
docs(error): clarify 422 vs 500 distinction
```

## Self-Review Checklist Pre-Push

- [ ] `git diff --stat` menunjukkan hanya file yang direncanakan.
- [ ] Tidak ada `console.log`, `print()`, `TODO` yang ditinggal.
- [ ] Tidak ada perubahan tak sengaja di lockfile / formatter.
- [ ] Test baru benar-benar gagal sebelum fix (bukti tes valid).
- [ ] Test pass setelah fix.
- [ ] Lint + format + typecheck pass.
- [ ] Diff jelas dibaca per commit (`git log -p`).
