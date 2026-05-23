# Stage 04 — Local Setup → Setup Log

**Code:** `LS` | **Output:** `SL-<repo>-001`

## Purpose
Memastikan Anda bisa **build + test + run** repo secara lokal, dengan langkah yang ter-dokumentasi sehingga reproducible.

## DoR
- [ ] Issue Brief `TAKE`.

## DoD
- [ ] Setup Log: command yang berhasil, command yang gagal + workaround, versi tooling (Node, Python, dst), env var, fixture data, cara menjalankan test suite full.
- [ ] `make test` (atau equivalent) hijau di lingkungan Anda.
- [ ] Branch kerja dibuat: `<your-name>/<issue#>-<short-slug>`.

---

## Prompt Template

```
1. ROLE
You are a build engineer who turns "works on my machine" into reproducible setup notes.

2. CONTEXT
Saya menyiapkan local environment untuk kontribusi.

3. INPUT
- README + CONTRIBUTING setup section:
{{paste}}
- Lingkungan saya: OS {{...}}, Node/Python/Go/Rust {{versi}}.
- Error pertama yang muncul: {{tempel}}.

4. TASK
- Sarankan langkah setup minimal hingga `test` hijau.
- Jika error: hipotesis penyebab + perintah diagnosa.
- Cek: container/devcontainer/nix tersedia? Pakai itu kalau ada.
- Cek: pre-commit hooks aktif? Install dulu.

5. OUTPUT
04-setup-log.md.

6. CONSTRAINTS
- Catat command persis (copy-pasteable).
- Catat versi tooling exact.

7. ACCEPTANCE
- [ ] Setup reproducible step-by-step.
- [ ] Test suite hijau (atau scope yang relevan).
```

---

## Artifact Template — `SL-<repo>-001`

```markdown
# Setup Log — {{owner/repo}}

| Field | Value |
|---|---|
| ID | SL-{{repo-slug}}-001 |
| OS | macOS 14.5 / Ubuntu 24.04 / Windows 11 + WSL2 |
| Date | {{YYYY-MM-DD}} |

## 1. Tooling Versions
| Tool | Version | How verified |
|---|---|---|
| Node | 20.12.0 | `node -v` |
| pnpm | 9.0.0 | `pnpm -v` |
| Python | 3.11.7 | `python --version` |
| Docker | 25.0 | `docker --version` |

## 2. Steps That Worked
```bash
git clone https://github.com/{{owner}}/{{repo}}
cd {{repo}}
git checkout -b <me>/<issue#>-<slug>

# install
pnpm install --frozen-lockfile

# pre-commit / hooks
pnpm prepare

# build
pnpm build

# test
pnpm test  # 412 passed, 0 failed
```

## 3. Errors & Fixes
| Error | Cause | Fix |
|---|---|---|
| `node-gyp` ERR | python missing | `xcode-select --install`; set `npm config set python python3` |
| Test `db.spec.ts` timeout | Postgres tidak jalan | `docker compose up -d db` |

## 4. Env Vars / Fixtures
| Var | Source | Value (dev) |
|---|---|---|
| `DATABASE_URL` | `.env.example` | `postgres://dev:dev@localhost:5432/app` |
| `JWT_SECRET` | docs | `dev-secret` |

Fixture data:
- `pnpm db:seed` — load 100 sample users.

## 5. Editor & Hooks
- ESLint + Prettier on save (`.vscode/settings.json` di repo).
- Husky pre-commit aktif.

## 6. Smoke Test
- `pnpm dev` → http://localhost:3000 = ✅ login screen.
- `pnpm test` = 412 passed.
- `pnpm typecheck` = no errors.

## 7. Branch
- Branch kerja: `me/123-fix-cli-help-text`.
- Base: `main` at commit `{{sha}}`.
```
