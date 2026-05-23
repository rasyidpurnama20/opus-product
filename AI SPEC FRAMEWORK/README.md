# AI SPEC FRAMEWORK

Framework prompt **berbasis artifact** untuk pengembang aplikasi yang bekerja bersama AI coding assistant (Kiro, Claude, Cursor, Copilot, dll).

Tujuan framework ini:
- Menyediakan **urutan tahapan baku** dalam siklus pengembangan aplikasi.
- Mendefinisikan **artifact** (dokumen / output) yang dihasilkan tiap tahap.
- Menyediakan **prompt template** yang konsisten dan reusable.
- Menjamin **traceability**: setiap baris kode bisa dilacak ke artifact, artifact bisa dilacak ke kebutuhan bisnis.

---

## 1. Prinsip Dasar

| Prinsip | Penjelasan |
|---|---|
| **Artifact-First** | Setiap tahap *wajib* menghasilkan artifact terdokumentasi. AI tidak loncat ke kode tanpa artifact upstream. |
| **Single Source of Truth** | Setiap informasi hanya hidup di satu artifact. Stage berikutnya *merujuk*, tidak menggandakan. |
| **Deterministic Prompt** | Prompt template punya struktur baku: `Role → Context → Input Artifact → Task → Output Artifact → Constraints → Acceptance`. |
| **Progressive Refinement** | Output stage N adalah input stage N+1. Tidak boleh skip. |
| **Reviewable** | Setiap artifact harus bisa di-review manusia sebelum lanjut ke tahap berikutnya. |

---

## 2. Tahapan (Stages)

Total 8 stage utama, urut, masing-masing punya nama baku, owner, input, dan output artifact.

```
┌──────────────────────────────────────────────────────────────────────────┐
│                        AI SPEC FRAMEWORK FLOW                            │
└──────────────────────────────────────────────────────────────────────────┘

  [01-Discovery]  ──►  Vision Brief (VB)
        │
        ▼
  [02-Requirements] ──►  Product Requirements Doc (PRD) + User Stories (US)
        │
        ▼
  [03-Architecture] ──►  Architecture Doc (ARCH) + ADR
        │
        ▼
  [04-Design]       ──►  Data Model (DM) + API Spec (OAS) + UI Spec (UIS)
        │
        ▼
  [05-Planning]     ──►  Task Breakdown (TB)
        │
        ▼
  [06-Implementation] ──►  Source Code + Inline Spec
        │
        ▼
  [07-Verification]  ──►  Test Plan (TP) + Test Report (TR)
        │
        ▼
  [08-Release]       ──►  Release Notes (RN) + Runbook (RB)
```

| # | Stage Code | Nama | Output Artifact | Code |
|---|---|---|---|---|
| 01 | `DSC` | Discovery | Vision Brief | `VB` |
| 02 | `REQ` | Requirements | Product Requirements Doc + User Stories | `PRD`, `US` |
| 03 | `ARC` | Architecture | Architecture Doc + Architecture Decision Records | `ARCH`, `ADR` |
| 04 | `DES` | Design | Data Model + OpenAPI Spec + UI Spec | `DM`, `OAS`, `UIS` |
| 05 | `PLN` | Planning | Task Breakdown | `TB` |
| 06 | `IMP` | Implementation | Source Code + Inline Spec | `SRC` |
| 07 | `VER` | Verification | Test Plan + Test Report | `TP`, `TR` |
| 08 | `REL` | Release | Release Notes + Runbook | `RN`, `RB` |

> Konvensi penamaan dokumen lengkap ada di [`00-conventions/naming.md`](./00-conventions/naming.md).

---

## 3. Struktur Folder

```
AI SPEC FRAMEWORK/
├── README.md                       ← file ini
├── 00-conventions/
│   ├── naming.md                   ← konvensi nama artifact, file, ID
│   ├── prompt-anatomy.md           ← struktur baku prompt
│   └── glossary.md                 ← istilah & singkatan
├── 01-discovery/
│   ├── README.md                   ← tujuan, input, output, definition of done
│   ├── prompt.md                   ← prompt template stage ini
│   └── artifact-template.md        ← template Vision Brief
├── 02-requirements/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
├── 03-architecture/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
├── 04-design/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
├── 05-planning/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
├── 06-implementation/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
├── 07-verification/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
├── 08-release/
│   ├── README.md
│   ├── prompt.md
│   └── artifact-template.md
└── examples/
    └── todo-app/                   ← contoh end-to-end fitur kecil
```

---

## 4. Cara Pakai

1. **Mulai dari Stage 01-Discovery.** Jangan loncat.
2. Buka folder stage, baca `README.md` untuk memahami input & output.
3. Salin isi `prompt.md`, isi placeholder `{{...}}`, kirim ke AI.
4. AI menghasilkan artifact mengikuti `artifact-template.md`.
5. **Review manusia** → revisi → simpan artifact di repo (folder `docs/specs/<feature>/`).
6. Lanjut ke stage berikutnya dengan artifact sebelumnya sebagai input.

---

## 5. Definition of Ready & Done per Stage

Setiap stage punya:
- **Definition of Ready (DoR):** syarat artifact upstream sudah lengkap & disetujui.
- **Definition of Done (DoD):** kriteria artifact stage ini boleh dianggap selesai.

Detail DoR/DoD ada di tiap `README.md` stage.

---

## 6. Quick Reference

| Saya butuh… | Buka… |
|---|---|
| Memulai fitur baru dari nol | `01-discovery/` |
| Menulis spec teknis | `03-architecture/` + `04-design/` |
| Memecah pekerjaan jadi task | `05-planning/` |
| Generate kode dari spec | `06-implementation/` |
| Membuat test | `07-verification/` |
| Rilis ke production | `08-release/` |
| Cek penamaan file/ID | `00-conventions/naming.md` |
| Cek struktur prompt | `00-conventions/prompt-anatomy.md` |

---

**Versi:** 1.0.0
**Lisensi:** Internal use
