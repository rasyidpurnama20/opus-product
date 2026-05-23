# Naming Conventions

Konvensi penamaan ini wajib dipakai di seluruh artifact framework agar bisa di-trace lintas stage.

## 1. Stage Code

| Code | Stage |
|---|---|
| `DSC` | Discovery |
| `REQ` | Requirements |
| `ARC` | Architecture |
| `DES` | Design |
| `PLN` | Planning |
| `IMP` | Implementation |
| `VER` | Verification |
| `REL` | Release |

## 2. Artifact Code

| Code | Artifact | Stage |
|---|---|---|
| `VB` | Vision Brief | DSC |
| `PRD` | Product Requirements Document | REQ |
| `US` | User Story | REQ |
| `ARCH` | Architecture Document | ARC |
| `ADR` | Architecture Decision Record | ARC |
| `DM` | Data Model | DES |
| `OAS` | OpenAPI Spec | DES |
| `UIS` | UI Spec | DES |
| `TB` | Task Breakdown | PLN |
| `SRC` | Source Code | IMP |
| `TP` | Test Plan | VER |
| `TR` | Test Report | VER |
| `RN` | Release Notes | REL |
| `RB` | Runbook | REL |

## 3. ID Format

Pola umum: `<ARTIFACT>-<FEATURE>-<NNN>`

- `<ARTIFACT>`: kode artifact, huruf kapital. Contoh: `US`, `ADR`.
- `<FEATURE>`: slug fitur singkat, lowercase, kebab-case. Contoh: `auth`, `cart-checkout`.
- `<NNN>`: nomor urut 3 digit dalam fitur tsb, mulai `001`.

Contoh:
- `US-auth-001` — User story pertama untuk fitur auth.
- `ADR-cart-checkout-002` — ADR kedua di fitur cart-checkout.
- `DM-billing-001` — Data model billing.

## 4. File Naming

```
<artifact-code-lower>-<feature-slug>-<nnn>.md
```

Contoh:
- `vb-auth-001.md`
- `prd-cart-checkout-001.md`
- `adr-billing-002.md`

OpenAPI dan SQL pakai ekstensi natif:
- `oas-billing-001.yaml`
- `dm-billing-001.sql`

## 5. Folder Layout di Repo Aplikasi

```
docs/
└── specs/
    └── <feature-slug>/
        ├── 01-discovery/
        │   └── vb-<feature>-001.md
        ├── 02-requirements/
        │   ├── prd-<feature>-001.md
        │   └── us-<feature>-001.md
        ├── 03-architecture/
        │   ├── arch-<feature>-001.md
        │   └── adr-<feature>-001.md
        ├── 04-design/
        │   ├── dm-<feature>-001.md
        │   ├── oas-<feature>-001.yaml
        │   └── uis-<feature>-001.md
        ├── 05-planning/
        │   └── tb-<feature>-001.md
        ├── 07-verification/
        │   ├── tp-<feature>-001.md
        │   └── tr-<feature>-001.md
        └── 08-release/
            ├── rn-<feature>-001.md
            └── rb-<feature>-001.md
```

> Stage 06 (Implementation) tidak punya folder `docs/`-nya sendiri; output-nya adalah source code di repo.

## 6. Status Tag

Tiap artifact punya header `Status` dengan nilai:

- `DRAFT` — masih dikerjakan.
- `IN_REVIEW` — siap di-review.
- `APPROVED` — disetujui, boleh dipakai stage berikutnya.
- `DEPRECATED` — sudah tidak relevan, tetap disimpan untuk histori.

## 7. Versioning

- Setiap artifact punya field `Version` (semver: `MAJOR.MINOR.PATCH`).
- `MAJOR` naik jika ada breaking change pada interpretasi artifact.
- `MINOR` naik jika ada penambahan substansial.
- `PATCH` naik untuk perbaikan editorial.

## 8. Cross-Reference

Saat artifact merujuk artifact lain, gunakan ID-nya:

> "Implements `US-auth-003`, depends on `ADR-auth-001`."
