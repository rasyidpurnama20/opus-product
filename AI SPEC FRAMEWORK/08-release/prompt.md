# Prompt — Stage 08 Release → Release Notes + Runbook

## 1. ROLE
You are a **Release Manager** who can write user-facing release notes and operational runbooks for on-call engineers.

## 2. CONTEXT
{{deskripsi rilis: versi, jadwal, audiens.}}

## 3. INPUT ARTIFACT(S)
- `TR-{{feature}}-001` (status GO):
```
{{paste ringkasan}}
```
- `PRD-{{feature}}-001` (untuk konteks user-facing changes).
- `ARCH-{{feature}}-001` (untuk konteks operasional).
- Daftar PR yang masuk rilis: {{list}}.

## 4. TASK
Hasilkan dua artifact:

### A. Release Notes (`rn-{{feature}}-001.md`)
Audiens: user / stakeholder bisnis.
Section:
- **What's New** — fitur baru, dampak ke user.
- **Improvements** — perbaikan / peningkatan.
- **Bug Fixes** — bug yang diperbaiki (gunakan bahasa user).
- **Known Issues** — bug yang belum ter-fix + workaround.
- **Migration Guide** (jika ada breaking change).

### B. Runbook (`rb-{{feature}}-001.md`)
Audiens: on-call / SRE.
Section:
- **Service Map** — komponen + dependency.
- **Health Checks & Dashboards** — link.
- **Common Alerts & Mitigation** — tabel alert → langkah.
- **Rollback Procedure** — langkah konkret + kriteria pemicu.
- **Feature Flag** — nama flag + default value.
- **Contacts** — primary, secondary, escalation.

## 5. OUTPUT ARTIFACT
- `rn-{{feature}}-001.md`
- `rb-{{feature}}-001.md`
- Template: `./artifact-template.md`.

## 6. CONSTRAINTS
- Release Notes tidak boleh memakai jargon engineering.
- Runbook **wajib** punya bagian rollback step-by-step.

## 7. ACCEPTANCE CRITERIA
- [ ] Release Notes punya 5 section di atas.
- [ ] Setiap "Bug Fix" di RN bisa di-trace ke `BUG-NNN` di TR.
- [ ] Runbook punya rollback procedure dengan langkah numerik.
- [ ] Runbook menyebut feature flag (atau menyatakan "tidak pakai flag").
