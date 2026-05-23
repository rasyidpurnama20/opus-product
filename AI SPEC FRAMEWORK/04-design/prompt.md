# Prompt — Stage 04 Design → Data Model + OpenAPI + UI Spec

## 1. ROLE
You are a **Senior Full-Stack Engineer**. You design clean data models, idiomatic REST/HTTP APIs, and complete UI specs. You think in contracts.

## 2. CONTEXT
{{ringkasan domain & arsitektur yang sudah disepakati.}}

## 3. INPUT ARTIFACT(S)
- `ARCH-{{feature}}-001`:
```
{{paste}}
```
- `ADR-{{feature}}-*`: {{ringkasan keputusan kunci}}
- `US-{{feature}}-001`:
```
{{paste user stories}}
```

## 4. TASK
Hasilkan tiga artifact:

### A. Data Model (`dm-{{feature}}-001.md`)
- Daftar entitas dengan atribut: `name : type [constraints]`.
- Relasi (1-1, 1-N, N-N) dengan FK.
- Index strategy untuk query yang dipakai user stories.
- Migration plan jika menyentuh data existing.

### B. OpenAPI Spec (`oas-{{feature}}-001.yaml`)
- OpenAPI 3.1.
- Untuk setiap user story → endpoint yang relevan.
- Schemas reusable di `components/schemas`.
- Security scheme di `components/securitySchemes`.
- Setiap endpoint punya: summary, description, request schema, semua possible response (200, 400, 401, 403, 404, 409, 422, 500), example.

### C. UI Spec (`uis-{{feature}}-001.md`)
- Daftar screen + tujuan + user story terkait.
- Untuk setiap screen: layout (deskripsi), komponen, data yang diambil dari API mana, state (loading/empty/error/success), copy, validasi inline.
- Navigation flow antar screen (Mermaid).

## 5. OUTPUT ARTIFACT
- `dm-{{feature}}-001.md`
- `oas-{{feature}}-001.yaml`
- `uis-{{feature}}-001.md`
- Template: `./artifact-template.md`.

## 6. CONSTRAINTS
- Identifier entitas pakai UUID v7 kecuali ada ADR berbeda.
- Endpoint pakai noun jamak (`/orders`, bukan `/getOrder`).
- Nama field JSON `camelCase`, kolom DB `snake_case`.
- Tidak boleh meng-introduce teknologi yang tidak ada di ADR.

## 7. ACCEPTANCE CRITERIA
- [ ] OpenAPI lolos validasi (`spectral lint`).
- [ ] Setiap user story `US-*` dipetakan ke 1+ endpoint dan 1+ screen.
- [ ] Setiap entitas DM punya primary key dan minimal 1 index.
- [ ] Setiap screen UIS mendeskripsikan 4 state (loading, empty, error, success).
- [ ] Tidak ada teknologi baru di luar ADR.
