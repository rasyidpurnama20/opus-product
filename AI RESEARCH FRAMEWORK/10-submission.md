# Stage 10 — Submission → Submission Pack

**Code:** `SU` | **Output:** `SUB-<paper-slug>-001`

## Purpose
Mempersiapkan **paket submission lengkap**: paper, supplementary, cover letter, reproducibility checklist, formatting, sesuai venue.

## DoR
- [ ] Draft Paper `READY`.

## DoD
- [ ] Submission Pack memuat: paper PDF (formatting venue), supplementary, cover letter (jika venue minta), reproducibility checklist, anonymization (untuk double-blind), supplementary code.
- [ ] Submitted via portal venue.

---

## Prompt Template

```
1. ROLE
You are a submission coordinator. You catch the small things that get papers desk-rejected.

2. CONTEXT
Saya akan submit ke {{venue}} dengan deadline {{date}}.

3. INPUT
- DP-{{slug}}-001: {{paste outline}}
- Venue submission instructions: {{paste link & key rules}}
- Format: LaTeX template venue.

4. TASK
- Cek formatting: page limit, font, margin, citation style.
- Sketsa cover letter (kalau venue minta).
- Sketsa reproducibility checklist sesuai venue (NeurIPS punya, ICML punya, ACL punya).
- Anonymize: cek nama author/affiliation, GitHub link, acknowledgment.
- Supplementary content: code repo (anonymized), data prep scripts, extra ablation, proofs.
- Pre-flight checklist akhir.

5. OUTPUT
10-submission-pack.md + folder submission/.

6. CONSTRAINTS
- Page limit STRICT.
- Anonymization STRICT untuk double-blind.
- Tidak boleh mengirim ke 2 venue bersamaan kalau larangan venue.

7. ACCEPTANCE
- [ ] Format venue compliant.
- [ ] Anonymization clean.
- [ ] Reproducibility statement filed.
- [ ] Supplementary lengkap.
```

---

## Artifact Template — `SUB-<paper-slug>-001`

```markdown
# Submission Pack — {{Working Title}}

| Field | Value |
|---|---|
| ID | SUB-{{slug}}-001 |
| Venue | {{NeurIPS 2026}} |
| Track | Main / Datasets & Benchmarks / Workshop |
| Deadline | {{2026-05-22 23:59 AoE}} |

## 1. Format Compliance
| Check | Required | Status |
|---|---|---|
| Page limit (excl. ref) | 9 | 8.5 ✅ |
| Font / template | venue's | using NeurIPS 2025 template |
| Citation style | venue's | natbib + venue.bst |
| Margins | venue's | unchanged |
| Anonymous (double-blind) | YES | author block removed; ack removed |
| Code anonymized | YES | new repo `anon-xxxx` |

## 2. Anonymization Audit
- [ ] No author names anywhere (incl. PDF metadata).
- [ ] No affiliation logos.
- [ ] Acknowledgments removed.
- [ ] GitHub links anonymized.
- [ ] Self-cite without revealing.
- [ ] Funding info redacted.

## 3. Reproducibility Checklist (venue-specific)
- [ ] All claims have linked evidence.
- [ ] Hyperparameter tuning protocol described.
- [ ] Seeds and number of runs reported.
- [ ] Compute resources stated.
- [ ] Code link provided (anon).
- [ ] Dataset access procedure described.
- [ ] License of all assets stated.

## 4. Supplementary
- `supp.pdf` — extra ablations, proofs, derivations.
- `code.zip` — anon repo at frozen commit.
- `data_prep.zip` — scripts to download + verify.
- `appendix_failures.pdf` — failure case gallery.

## 5. Cover Letter (kalau venue minta)
{{1 halaman: ringkas kontribusi, mengapa cocok venue, list reviewer yang harus di-konflik (collaborator, advisor lab).}}

## 6. Pre-Flight (24 jam sebelum deadline)
- [ ] Compile PDF di TeX live versi venue.
- [ ] Open PDF di Acrobat & Preview — figure tidak rusak.
- [ ] Check PDF metadata (Producer, Creator) tidak bocor identitas.
- [ ] Test upload supplementary (size limit?).
- [ ] Review submission portal fields lengkap.
- [ ] Notify co-author untuk approval final.
- [ ] Save confirmation receipt.

## 7. Backup
- Tag git repo: `submission-{{venue}}-2026`.
- Archive folder: `submissions/{{venue}}-2026/{{slug}}/` (paper, supp, code, configs, results).
```
