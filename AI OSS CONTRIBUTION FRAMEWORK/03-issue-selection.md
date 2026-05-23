# Stage 03 — Issue Selection → Issue Brief

**Code:** `IS` | **Output:** `IB-<repo>-<issue#>`

## Purpose
Memilih issue/feature yang **tepat ukurannya** untuk Anda saat ini, dan memastikan ekspektasi maintainer jelas sebelum coding.

## DoR
- [ ] Codebase Map dipahami secara umum.

## DoD
- [ ] Issue Brief memuat: issue link, original ask, scope yang Anda interpretasikan, ukuran (S/M/L), risk, signal dari maintainer (sudah claimed? duplicate?).
- [ ] Anda menulis komen di issue (untuk OSS publik) untuk meminta assignment / mengkonfirmasi pendekatan **sebelum** coding (kecuali fix trivial).

---

## Prompt Template

```
1. ROLE
You are an OSS contributor coach. You stop people from wasting time on the wrong issues.

2. CONTEXT
Saya sudah punya peta repo. Sekarang saya pilih issue.

3. INPUT
- Issue: {{link issue}} atau:
  Title: {{...}}
  Body: {{...}}
  Labels: {{...}}
  Comments so far: {{...}}
- Tujuan saya: {{quick win / belajar / fitur prioritas saya}}.
- Skill saya: {{...}}.

4. TASK
- Ringkas inti masalah/fitur dalam 3 kalimat.
- Klasifikasi tipe: bug / feature / docs / refactor / chore.
- Ukur scope: S (≤ 4 jam), M (≤ 2 hari), L (≤ 1 minggu), XL (terlalu besar untuk solo).
- Cek: ada PR yang sudah claim? assigned? duplicate?
- Identifikasi pertanyaan yang harus dijawab maintainer sebelum mulai.
- Sarankan komen kalimat singkat untuk meminta assignment / konfirmasi pendekatan.
- Recommend: TAKE / SKIP / ASK FIRST.

5. OUTPUT
03-issue-brief-{{issue#}}.md.

6. CONSTRAINTS
- Tidak menulis kode.
- Komen ke maintainer harus sopan, ringkas, profesional.

7. ACCEPTANCE
- [ ] Scope ukuran tegas.
- [ ] Cek duplicate / claimed.
- [ ] Komen pre-work disiapkan.
```

---

## Artifact Template — `IB-<repo>-<issue#>`

```markdown
# Issue Brief — {{owner/repo}}#{{issue#}}

| Field | Value |
|---|---|
| ID | IB-{{repo-slug}}-{{issue#}} |
| Issue link | https://github.com/{{owner}}/{{repo}}/issues/{{N}} |
| Type | bug / feature / docs / refactor |
| Size | S / M / L / XL |
| Priority signal | maintainer-flagged / community / mine |

## 1. Original Ask
> {{paste judul + isi singkat issue}}

## 2. My Interpretation
{{Apa yang sebenarnya diminta, dari sudut pandang implementasi.}}

## 3. Scope
- **In scope:** {{...}}
- **Out of scope:** {{...}}
- **Estimasi:** {{X jam / hari}}.

## 4. Existing Activity
- Open PR yang adress ini: {{none / #123 (stale) / #145 (active)}}.
- Comments dari maintainer: {{ringkasan, ada keputusan? ada batasan?}}.
- Duplicate of: {{none / #88}}.

## 5. Open Questions for Maintainer
- {{Q1: pendekatan A vs B?}}
- {{Q2: harus backward compatible?}}
- {{Q3: target di branch main atau release-x?}}

## 6. Pre-Work Comment (untuk issue)
> Hi maintainers, saya tertarik mengerjakan #{{N}}. Pendekatan yang saya pikirkan: {{ringkas 2 kalimat}}.
> Apakah pendekatan ini selaras dengan visi project? Boleh saya assign untuk ini? Estimasi {{X}} hari.

## 7. Decision
- **TAKE / SKIP / ASK FIRST:** {{...}}
- **Reason:** {{...}}
```
