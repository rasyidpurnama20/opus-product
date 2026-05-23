# Stage 01 — Project Discovery → Project Brief

**Code:** `PD` | **Output:** `PB-<repo>-001`

## Purpose
Memutuskan apakah project ini layak Anda investasikan waktu. Cek kesehatan, lisensi, governance, ekspektasi reviewer.

## DoR
- [ ] Anda punya kandidat repo URL.

## DoD
- [ ] Project Brief memuat: maintenance health, license compatibility, governance model, contribution culture, response time, "good first issue" availability, rough fit dengan tujuan Anda.
- [ ] Keputusan: GO / NO-GO untuk lanjut ke stage 02.

---

## Prompt Template

```
1. ROLE
You are an experienced open-source contributor and OSS health auditor.

2. CONTEXT
Saya berniat berkontribusi ke / fork / memodifikasi repo ini untuk: {{tujuan}}.

3. INPUT
- Repo: https://github.com/{{owner}}/{{repo}}
- Saya punya akses ke: README, CONTRIBUTING, CODE_OF_CONDUCT, GOVERNANCE, LICENSE, recent issues & PRs.
- Tujuan saya: {{contribute fitur X / fix bug Y / fork untuk pakai internal / belajar}}.

4. TASK
Bantu saya menyusun Project Brief:
- Ringkas tujuan & domain repo (3 kalimat).
- Cek lisensi (MIT, Apache-2.0, GPL, AGPL, custom) dan kompatibilitas dengan rencana saya.
- Health metric: jumlah maintainer aktif, frekuensi commit, median time-to-respond untuk issues, %merge rate untuk PR luar.
- Governance: BDFL / committee / corp-backed / fully community.
- Contribution culture: ada CONTRIBUTING.md? CLA / DCO? "good first issue"? code review style?
- Risiko: stale, hostile maintainer, license change, vendor lock.
- Rekomendasi: GO / NO-GO + alasan.

5. OUTPUT
01-project-brief.md.

6. CONSTRAINTS
- Tidak boleh asumsi kalau dokumen tidak ada — tandai "NOT FOUND".
- Health metric harus dari data observable (commits, issue/PR list).

7. ACCEPTANCE
- [ ] License & compatibility tegas dijawab.
- [ ] 3+ health metric numerik atau "tidak diketahui".
- [ ] GO/NO-GO decision dengan alasan.
```

---

## Artifact Template — `PB-<repo>-001`

```markdown
# Project Brief — {{owner/repo}}

| Field | Value |
|---|---|
| ID | PB-{{repo-slug}}-001 |
| Status | DRAFT |
| Date | {{YYYY-MM-DD}} |
| URL | https://github.com/{{owner}}/{{repo}} |

## 1. Summary
{{Apa yang dilakukan repo ini, audiens, posisi di ekosistem.}}

## 2. License
- License: MIT / Apache-2.0 / GPL-3.0 / AGPL / proprietary.
- Compatible with my use ({{commercial / closed-source / fork-redist}}): YES / NO.
- CLA / DCO required: YES / NO.

## 3. Health Metrics
| Metric | Value |
|---|---|
| Stars | {{...}} |
| Forks | {{...}} |
| Active maintainers (last 90 days) | {{N}} |
| Commit frequency | {{N/week}} |
| Open issues | {{N}} |
| Median time-to-first-response (issue) | {{X days}} |
| Open PRs | {{N}} |
| External-PR merge rate (last 50) | {{X%}} |

## 4. Governance
- Model: {{BDFL / steering committee / Linux-style / corp-led}}.
- Decision process: {{...}}.
- Maintainers list: {{...}}.

## 5. Contribution Culture
- CONTRIBUTING.md: YES / NO. Key requirements: {{...}}.
- Code of Conduct: YES / NO.
- "good first issue" / "help wanted" labels: YES / NO. Count: {{N}}.
- Code review style: {{strict & long / lightweight}}.
- Average review iterations: {{N}}.

## 6. Risk Assessment
| Risk | Severity | Note |
|---|---|---|
| Stale (no commit > 6m) | low/med/high | |
| Hostile / unresponsive maintainer | low/med/high | based on tone in issues |
| License change history | low/med/high | |
| Vendor lock-in (corp-only contributors) | low/med/high | |

## 7. Decision
- **GO / NO-GO:** {{...}}
- **Reason:** {{...}}
- **If GO, time budget:** {{X hours/week, Y weeks}}.
```
