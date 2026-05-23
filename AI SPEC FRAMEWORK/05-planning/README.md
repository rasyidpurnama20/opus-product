# Stage 05 — Planning

**Code:** `PLN`
**Output Artifact:** Task Breakdown (`TB`)

## Tujuan
Memecah user stories + design artifacts menjadi task-task kecil yang independen, dapat diestimasi, dan siap dieksekusi.

## Owner
Tech Lead. AI berperan sebagai *task decomposer*.

## Input
- `US-<feature>` (`APPROVED`).
- `DM`, `OAS`, `UIS` (`APPROVED`).
- `ARCH` + ADRs.

## Output
- `tb-<feature>-001.md` — Task Breakdown dengan ID `T-<feature>-NNN`.

## DoR
- [ ] Stage 02 + 03 + 04 selesai dan `APPROVED`.

## DoD
- [ ] Setiap task punya: ID, judul, deskripsi, acceptance criteria, dependency, estimasi (S/M/L), linked artifact.
- [ ] Setiap user story tercakup oleh ≥ 1 task.
- [ ] Tidak ada task lebih besar dari `L` (≈ 1 hari kerja). Pecah jika terlalu besar.

## Anti-Pattern
- Task berbentuk "selesaikan fitur X" tanpa pecahan.
- Task tanpa acceptance criteria.
- Estimasi tidak konsisten.
