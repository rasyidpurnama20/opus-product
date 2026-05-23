# Stage 10 — Review Iteration → Review Response Log

**Code:** `RI` | **Output:** `RRL-<repo>-<issue#>`

## Purpose
Menanggapi komen reviewer dengan profesional, sistematis, tanpa lupa atau nyolot. PR yang merge biasanya butuh 2–5 iterasi review.

## DoR
- [ ] PR submitted, ada komen reviewer.

## DoD
- [ ] Setiap komen reviewer di-track (accept / counter-propose / decline) dengan alasan.
- [ ] Setiap perubahan punya commit kecil ber-link ke komen.
- [ ] Setelah semua resolved, request re-review.

---

## Prompt Template

```
1. ROLE
You are a contributor responding to PR feedback graciously and competently.
You don't argue for ego; you argue for code.

2. CONTEXT
PR saya dapat review.

3. INPUT
- PR: {{link}}
- Komen reviewer:
{{paste komen-komen}}

4. TASK
Untuk tiap komen:
- Klasifikasi: ACCEPT / COUNTER / CLARIFY / DEFER (out of scope).
- Kalau ACCEPT: tulis perubahan kode + draft balasan singkat.
- Kalau COUNTER: tulis argumen 1 paragraf, sertakan data/contoh.
- Kalau CLARIFY: tulis pertanyaan netral.
- Kalau DEFER: usulkan follow-up issue.

5. OUTPUT
10-review-log-{{issue#}}.md.

6. CONSTRAINTS
- Bahasa: ramah, profesional, "we" / "let's" friendly.
- Tidak defensif, tidak sarkastis.
- Jangan ubah kode di luar yang diminta sambil lalu.

7. ACCEPTANCE
- [ ] Setiap komen punya respons.
- [ ] Setiap perubahan punya commit kecil yang me-reference komen.
```

---

## Artifact Template — `RRL-<repo>-<issue#>`

```markdown
# Review Response Log — {{owner/repo}}#{{issue#}}

| Field | Value |
|---|---|
| ID | RRL-{{repo-slug}}-{{issue#}} |
| PR | https://github.com/{{owner}}/{{repo}}/pull/{{N}} |
| Iterations | 2 (so far) |

## Round 1 — {{date}}

### Comment 1 — by @maintainer-a
> "Hmm, what about the case where validator throws non-Error (e.g., string)?"

- Classification: **ACCEPT**.
- Action: tambahkan test + handle non-Error throw → wrap ke `ValidationError`.
- Commit: `test+fix: handle non-Error validator throw (review feedback)`.
- Reply:
  > Good catch — added a guard to coerce non-Error throws into ValidationError. New test in `validate.test.ts > non-Error throw`. Pushed.

### Comment 2 — by @maintainer-b
> "Why not just use the global error handler we already have in `src/errors.ts`?"

- Classification: **CLARIFY**.
- Reply:
  > I considered routing through `src/errors.ts` (option C in PR description). I chose middleware-local because (1) it limits the diff, (2) the global handler currently maps everything to 500 — would need refactor, (3) preserves existing retry-middleware semantics for non-validation 5xx. Happy to switch if you'd prefer the broader change in this PR (would extend scope to ~150 LOC).

### Comment 3 — by @maintainer-a
> "Tests pass on Linux but I see `pathSeparator` magic — does this work on Windows?"

- Classification: **ACCEPT**.
- Action: switch to `path.sep`, add Windows test on CI matrix.
- Commit: `fix(test): use path.sep for cross-platform compat`.

### Comment 4 — by @maintainer-c (nit)
> "Prefer `unknown` over `any` here."

- Classification: **ACCEPT** (always do nits to keep momentum).
- Commit: `style: tighten error type to unknown`.

## Round 2 — {{date}}

### Comment 5
{{...}}

## Status
- All threads resolved: ✅
- Re-review requested: ✅
- CI green: ✅
- Final maintainer ping: "/review please" sent {{date}}.

## Lessons For Next PR
- Perlu jelaskan trade-off "broader vs localized fix" di PR description awal supaya tidak diulang di review.
- Selalu jalankan test di Windows VM kalau menyentuh path.
```
