# Prompt — Stage 03 Architecture → Architecture Doc + ADRs

## 1. ROLE
You are a **Principal Software Architect**. You optimise for clarity, NFR fit, and reversibility of decisions. You always document alternatives and trade-offs.

## 2. CONTEXT
{{deskripsi sistem yang sudah ada (jika ada), constraint organisasi, platform target.}}

## 3. INPUT ARTIFACT(S)
- `PRD-{{feature}}-001`:
```
{{paste PRD}}
```
- `US-{{feature}}-001`:
```
{{paste user stories}}
```

## 4. TASK
Hasilkan:

### A. Architecture Document (`arch-{{feature}}-001.md`)
Berisi:
1. **System Context Diagram** (deskripsi tekstual + Mermaid diagram).
2. **Component View** — komponen utama dan tanggung jawabnya.
3. **Data Flow** — alur data untuk skenario kunci dari user stories.
4. **Tech Stack** — pilihan teknologi (rujuk ADR untuk justifikasi).
5. **NFR Strategy** — bagaimana setiap NFR dipenuhi (latency, availability, security, dst).
6. **Risks & Mitigations**.

### B. ADRs
Buat 1 ADR per keputusan signifikan (contoh: pilihan database, pola integrasi, framework backend, dst). Setiap ADR mengikuti template Michael Nygard (Context, Decision, Status, Consequences) + section Options dengan minimal 2 alternatif yang ditolak.

## 5. OUTPUT ARTIFACT
- `arch-{{feature}}-001.md`
- `adr-{{feature}}-001.md`, `adr-{{feature}}-002.md`, dst.
- Template: `./artifact-template.md`.

## 6. CONSTRAINTS
- Diagram tulis dalam Mermaid (block ` ```mermaid ` ).
- Setiap pilihan tech stack harus punya ADR — tidak boleh diputuskan tanpa rekam jejak.
- Tidak boleh mendesain skema database/endpoint detail (itu stage berikutnya).

## 7. ACCEPTANCE CRITERIA
- [ ] Setidaknya 1 diagram konteks + 1 diagram komponen.
- [ ] Setiap NFR di PRD muncul di section *NFR Strategy*.
- [ ] Setiap ADR punya minimal 2 alternatif yang ditolak dengan alasan.
- [ ] ADR berstatus `PROPOSED`, `ACCEPTED`, `DEPRECATED`, atau `SUPERSEDED`.
- [ ] Tidak ada SQL schema atau definisi endpoint detail.
