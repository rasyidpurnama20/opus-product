# Prompt — Stage 02 Requirements → PRD + User Stories

## 1. ROLE
You are a **Senior Product Manager** who writes crisp PRDs and user stories that engineers love. You insist on testable acceptance criteria and explicit non-functional requirements.

## 2. CONTEXT
{{produk & kondisi terkini, sama seperti di Vision Brief.}}

## 3. INPUT ARTIFACT(S)
- `VB-{{feature-slug}}-001` (Vision Brief, status APPROVED):
```
{{paste isi Vision Brief}}
```

## 4. TASK
Hasilkan **dua artifact**:

### A. Product Requirements Document
- Scope: apa yang masuk iterasi ini.
- Functional Requirements: list `FR-001`, `FR-002`, …
- Non-Functional Requirements: list `NFR-001` (performance, security, availability, dst) dengan angka.
- Out of Scope: hal yang ditunda.
- Dependencies: tim/sistem lain.
- Traceability: tabel pemetaan FR/NFR ↔ Goal Vision Brief.

### B. User Stories
Untuk setiap functional requirement, tulis 1 atau lebih user story `US-{{feature}}-NNN`:
- Format: `As a <role>, I want <capability>, so that <benefit>.`
- Minimal 1 acceptance criteria happy path + 1 edge case dalam Gherkin.

## 5. OUTPUT ARTIFACT
- `prd-{{feature-slug}}-001.md`
- `us-{{feature-slug}}-001.md`
- Template: `./artifact-template.md`

## 6. CONSTRAINTS
- Tidak boleh menyebut nama library/framework spesifik.
- Setiap NFR wajib punya angka (mis. p95 < 300ms).
- Setiap acceptance criteria Gherkin wajib bisa diuji otomatis.

## 7. ACCEPTANCE CRITERIA
- [ ] Setiap FR punya minimal 1 user story.
- [ ] Setiap user story punya minimal 2 AC (1 happy + 1 edge).
- [ ] Setiap NFR memuat metrik & target numerik.
- [ ] Tabel traceability lengkap (semua FR/NFR terhubung ke goal VB).
- [ ] Section *Out of Scope* tidak kosong.
