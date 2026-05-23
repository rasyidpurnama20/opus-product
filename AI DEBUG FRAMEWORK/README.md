# AI DEBUG FRAMEWORK

Framework untuk **investigasi bug & insiden** secara sistematis. Lawan dari panic-debugging yang ngubah-ngubah random sampe kelihatan jalan.

## Prinsip
1. **Reproduce before fix.** Tidak ada fix tanpa repro yang reliable.
2. **One hypothesis at a time.** Ubah satu variabel, observasi.
3. **Bisect pakai data, bukan firasat.** `git bisect`, log timestamp, A/B configs.
4. **Root cause, bukan symptom.** "Ditambah retry" jangan jadi default fix.
5. **Prevent recurrence.** Setiap bug = test baru.

## Stages
```
[01-Capture] ──► [02-Repro] ──► [03-Hypothesis] ──► [04-Investigate] ──► [05-RCA] ──► [06-Fix] ──► [07-Postmortem]
```

| # | Stage | Output | Code |
|---|---|---|---|
| 01 | Symptom Capture | Bug Report | `BR` |
| 02 | Reproduction | Repro Recipe | `RR` |
| 03 | Hypothesis | Hypothesis Log | `HL` |
| 04 | Investigation | Investigation Log | `IL` |
| 05 | Root Cause | RCA Document | `RCA` |
| 06 | Fix | Fix + Regression Test | `FX` |
| 07 | Postmortem | Postmortem (incidents) | `PM` |
