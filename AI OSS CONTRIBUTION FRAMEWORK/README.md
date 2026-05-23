# AI OSS CONTRIBUTION FRAMEWORK

Framework untuk **berkontribusi atau memodifikasi project GitHub yang sudah ada**, baik untuk:
- Submit PR ke project orang lain (open source contribution).
- Fork & modifikasi untuk kebutuhan internal/personal.
- Maintain fork jangka panjang.

Beda dengan `AI SPEC FRAMEWORK` (membangun dari nol), di sini Anda **masuk ke kode orang lain** — yang punya konvensi, gaya, governance, dan emosi maintainer-nya sendiri. Frame Of Mind harus berubah: *humble, observasi dulu, ikuti gaya rumah*.

## Prinsip
1. **Read 10x more than you write.** Sebelum 1 baris diubah, baca repo.
2. **Smallest change that solves it.** PR raksasa = PR ditolak.
3. **Match house style.** Gaya kode mengikuti repo, bukan preferensi pribadi.
4. **Talk before code.** Untuk perubahan non-trivial, buka issue / discussion dulu.
5. **Tests are non-negotiable.** Project serius wajib test untuk PR diterima.
6. **Maintainer time is precious.** Buat reviewer mudah bilang "yes".

## Stages

```
[01-Discovery]    ──► Project Brief (PB)              ← apa repo ini, layak ikut?
       │
       ▼
[02-Recon]        ──► Codebase Map (CM)               ← arsitektur, gaya, hot spots
       │
       ▼
[03-Issue]        ──► Issue Brief (IB)                ← issue/feature target + scope
       │
       ▼
[04-Setup]        ──► Setup Log (SL)                  ← bisa build & test lokal
       │
       ▼
[05-Reproduction] ──► Repro Report (RR)               ← bug ter-konfirmasi (skip untuk feature)
       │
       ▼
[06-Plan]         ──► Change Plan (CP)                ← file yang disentuh, alternatif
       │
       ▼
[07-Implementation] ──► Patch (commits)               ← code + tests
       │
       ▼
[08-Validation]   ──► Validation Report (VR)          ← test/lint/manual checklist
       │
       ▼
[09-PR]           ──► PR Submission (PRS)             ← title, body, screenshots
       │
       ▼
[10-Iteration]    ──► Review Response Log (RRL)       ← per komen reviewer, keputusan
```

| # | Stage | Output | Code |
|---|---|---|---|
| 01 | Project Discovery | Project Brief | `PB` |
| 02 | Codebase Recon | Codebase Map | `CM` |
| 03 | Issue Selection | Issue Brief | `IB` |
| 04 | Local Setup | Setup Log | `SL` |
| 05 | Reproduction | Repro Report | `RR` |
| 06 | Change Plan | Change Plan | `CP` |
| 07 | Implementation | Patch (commits) | `PT` |
| 08 | Validation | Validation Report | `VR` |
| 09 | Pull Request | PR Submission | `PRS` |
| 10 | Review Iteration | Review Response Log | `RRL` |

## Konvensi ID
`<CODE>-<repo-slug>-<NNN>`. Contoh `PB-langchain-001`, `CP-langchain-007`.

## Folder Layout di Working Repo
Simpan artifact di branch lokal, jangan masuk ke PR:
```
.contrib/<repo-slug>/
├── 01-project-brief.md
├── 02-codebase-map.md
├── 03-issue-brief-<issue#>.md
├── 04-setup-log.md
├── 05-repro-report-<issue#>.md
├── 06-change-plan-<issue#>.md
├── 08-validation-<issue#>.md
├── 09-pr-submission-<issue#>.md
└── 10-review-log-<issue#>.md
```

> Tambahkan `.contrib/` ke `.gitignore` global / `info/exclude` agar tidak ikut PR.

## Anti-Pattern
- "Drive-by PR" — PR tanpa baca CONTRIBUTING.md / docs governance.
- Code style fight — re-format file di luar scope.
- PR menambah dependency tanpa diskusi.
- Mengabaikan komen reviewer / silent untuk minggu.
- Force-push tanpa pemberitahuan saat PR sudah di-review.
