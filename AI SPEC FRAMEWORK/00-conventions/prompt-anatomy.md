# Prompt Anatomy

Semua prompt template di framework ini mengikuti **7 blok baku**. Tujuannya: hasil AI deterministik, terukur, dan reviewable.

## Struktur Baku

```
1. ROLE
2. CONTEXT
3. INPUT ARTIFACT(S)
4. TASK
5. OUTPUT ARTIFACT
6. CONSTRAINTS
7. ACCEPTANCE CRITERIA
```

### 1. ROLE
Persona AI yang dipakai. Spesifik. Hindari "you are an AI assistant".

> Contoh: "You are a senior product manager with 10 years of experience in B2B SaaS."

### 2. CONTEXT
Latar belakang yang relevan: produk apa, user siapa, masalah apa, kondisi sekarang.

> Contoh: "Kami sedang membangun aplikasi tracking inventaris untuk UMKM toko kelontong di Indonesia."

### 3. INPUT ARTIFACT(S)
Artifact dari stage sebelumnya yang menjadi sumber kebenaran. Sertakan ID dan isi penuh / link.

> Contoh: "Input: `VB-inventory-001` (lihat lampiran)."

### 4. TASK
Instruksi spesifik yang harus dilakukan. Pakai kata kerja imperatif.

> Contoh: "Buat PRD lengkap berdasarkan Vision Brief di atas."

### 5. OUTPUT ARTIFACT
Artifact yang harus dihasilkan, lengkap dengan format file dan template yang diikuti.

> Contoh: "Output: dokumen Markdown mengikuti template `prd-template.md`, simpan sebagai `prd-inventory-001.md`."

### 6. CONSTRAINTS
Batasan teknis, gaya, panjang, bahasa, kepatuhan.

> Contoh:
> - Bahasa: Indonesia (istilah teknis boleh tetap Inggris).
> - Maksimal 1500 kata.
> - Tidak boleh menyebut teknologi spesifik di stage ini.

### 7. ACCEPTANCE CRITERIA
Kriteria objektif yang menentukan output diterima atau tidak. Reviewer pakai checklist ini.

> Contoh:
> - [ ] Setiap user story punya acceptance criteria Gherkin.
> - [ ] Tidak ada solusi teknis di section "Problem Statement".
> - [ ] Semua claim metrik punya angka target.

---

## Template Kosong

```markdown
# Prompt: <Stage> — <Output Artifact>

## 1. ROLE
{{role}}

## 2. CONTEXT
{{context}}

## 3. INPUT ARTIFACT(S)
- {{artifact_id_1}}: {{ringkasan_atau_link}}
- {{artifact_id_2}}: ...

## 4. TASK
{{task_description}}

## 5. OUTPUT ARTIFACT
- Format: {{markdown|yaml|sql}}
- Nama file: {{file-name}}
- Template: {{path/to/template}}

## 6. CONSTRAINTS
- {{constraint_1}}
- {{constraint_2}}

## 7. ACCEPTANCE CRITERIA
- [ ] {{criterion_1}}
- [ ] {{criterion_2}}
```

---

## Anti-Pattern

Hindari:
- Prompt tanpa Role spesifik ("you are helpful assistant").
- Task ambigu ("buat dokumen yang bagus").
- Tidak menyebut input artifact upstream → AI berhalusinasi konteks.
- Tidak ada acceptance criteria → tidak bisa di-review objektif.
- Mencampur banyak stage dalam satu prompt (mis. minta requirements + arsitektur + kode sekaligus).
