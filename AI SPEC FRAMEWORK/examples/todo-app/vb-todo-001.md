# Vision Brief — Personal Todo App

| Field | Value |
|---|---|
| ID | `VB-todo-001` |
| Status | `APPROVED` |
| Version | `1.0.0` |
| Author | Demo |
| Date | 2026-05-23 |

## 1. Problem Statement
Pengguna individu kesulitan mengingat tugas harian. Aplikasi catatan umum terasa berlebihan; pengguna butuh cara cepat menulis tugas dan menandai selesai. Survei internal menunjukkan 7 dari 10 pengguna lupa minimal 1 tugas penting per minggu.

## 2. Target User
- **Primary:** Knowledge worker individu, 22–40 tahun, biasa pakai smartphone.
- **Secondary:** Pelajar/mahasiswa.

## 3. Goals
| # | Goal | Metric | Baseline | Target | Timeframe |
|---|---|---|---|---|---|
| G1 | Menurunkan jumlah tugas yang terlupakan | tugas_lupa / minggu | 1 | ≤ 0.3 | Q3 2026 |
| G2 | Aktivasi user dalam D1 | % user buat ≥ 1 todo D1 | n/a | ≥ 60% | Q3 2026 |
| G3 | Retention 7 hari | % user aktif H+7 | n/a | ≥ 35% | Q3 2026 |

## 4. Non-Goals
- Kolaborasi tim / shared list.
- Reminder berbasis lokasi.
- Integrasi kalender pihak ketiga.

## 5. Assumptions & Risks
| # | Tipe | Deskripsi | Mitigasi |
|---|---|---|---|
| A1 | Asumsi | User mau membuka aplikasi minimal 1× sehari. | Reminder push notif sederhana. |
| R1 | Risiko | Pasar todo app sudah jenuh. | Fokus simplicity & speed. |
| R2 | Risiko | Sinkronisasi multi-device kompleks. | MVP single-device dulu. |

## 6. Open Questions
- Apakah perlu dukungan offline di MVP?

## 7. References
- Hasil survei internal Mei 2026.
