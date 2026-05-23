# Stage 02 — Codebase Recon → Codebase Map

**Code:** `CR` | **Output:** `CM-<repo>-001`

## Purpose
Memahami struktur, gaya, dan "hot spots" repo sebelum menyentuh apapun. Jangan mulai modifikasi sebelum tahu ekosistem internalnya.

## DoR
- [ ] Project Brief `GO`.

## DoD
- [ ] Codebase Map memuat: top-level layout, entry points, runtime/build/test commands, coding style cues, hot spots (file paling sering disentuh), dependency graph kasar, dokumen arsitektur (jika ada).

---

## Prompt Template

```
1. ROLE
You are a code archaeologist who maps unfamiliar codebases efficiently.

2. CONTEXT
Saya akan kontribusi ke repo {{owner/repo}}. Saya butuh peta sebelum dive in.

3. INPUT
- Repo sudah saya clone lokal: `{{path}}`.
- README + CONTRIBUTING:
{{paste excerpt}}
- Bahasa: {{TS / Python / Go / Rust / multi}}.

4. TASK
Bantu saya buat Codebase Map:
- Top-level folder layout dengan tanggung jawab tiap folder.
- Entry point (main, server, CLI, lib export).
- Build & test command (dari package.json, pyproject, Makefile, justfile, dll).
- Coding style cues (linter config, formatter, naming convention yang terlihat).
- Hot spot: file/modul yang paling sering disentuh berdasarkan git log.
- Tes structure: di mana, frameworknya apa, coverage style.
- Dependency graph kasar: modul apa depend ke apa.
- Dokumen arsitektur tersedia: ARCHITECTURE.md, ADR folder, design doc.

5. OUTPUT
02-codebase-map.md.

6. CONSTRAINTS
- Tidak menyarankan refactor.
- Untuk hot spot, sebut command git yang dipakai (mis. `git log --pretty=format: --name-only | sort | uniq -c | sort -rn | head -20`).

7. ACCEPTANCE
- [ ] Build + test command bisa dieksekusi user.
- [ ] Coding style cues teridentifikasi (lint config / formatter).
- [ ] 5–10 hot-spot file teridentifikasi.
```

---

## Artifact Template — `CM-<repo>-001`

```markdown
# Codebase Map — {{owner/repo}}

| Field | Value |
|---|---|
| ID | CM-{{repo-slug}}-001 |
| Status | DRAFT |
| Linked PB | PB-{{repo-slug}}-001 |
| Commit ref | {{git rev-parse HEAD}} |

## 1. Top-Level Layout
```
src/
  core/        ← domain logic, no I/O
  io/          ← adapters (HTTP, DB, FS)
  cli/         ← CLI entrypoints
tests/
  unit/
  integration/
docs/
examples/
```

## 2. Entry Points
| Type | File | Note |
|---|---|---|
| Library export | `src/index.ts` | public API |
| CLI | `bin/cli.js` | invoked via `npx repo-name` |
| Dev server | `pnpm dev` | calls `src/cli/dev.ts` |

## 3. Build & Test
| Command | Purpose |
|---|---|
| `pnpm install` | install deps |
| `pnpm build` | tsc → dist |
| `pnpm test` | vitest --run |
| `pnpm lint` | eslint + prettier check |
| `pnpm typecheck` | tsc --noEmit |

## 4. Coding Style Cues
- Linter: ESLint with `eslint:recommended` + custom rules in `.eslintrc.cjs`.
- Formatter: Prettier (2 spaces, single quote, no semicolon? cek).
- Naming: file `kebab-case.ts`, type `PascalCase`, fn `camelCase`.
- Imports: enforced order (builtin → ext → internal).
- Tests next to source as `*.test.ts` OR mirror in `tests/`.

## 5. Hot Spots
Run: `git log --since=12.months --pretty=format: --name-only | grep -v '^$' | sort | uniq -c | sort -rn | head -20`.

| File | Edit count |
|---|---|
| `src/core/scheduler.ts` | 142 |
| `src/io/http.ts` | 98 |
| ... | |

## 6. Test Structure
- Framework: vitest.
- Unit test: tests bisa di `src/**/*.test.ts`.
- Integration test: `tests/integration/`.
- Mock strategy: msw for HTTP, in-memory adapters for DB.

## 7. Dependency Graph (rough)
```
cli → core → io
core → utils
io → external libs (axios, prisma)
```

## 8. Architecture Docs
- `docs/ARCHITECTURE.md`: present, last updated {{date}}.
- ADR: `docs/adr/` — {{N}} files.
- Discord / Slack: {{link}}.

## 9. Open Questions
- Mengapa folder `legacy/` masih ada? (cek sebelum menyentuh).
- Apa yang berubah signifikan di v3 → v4 (lihat CHANGELOG).
```
