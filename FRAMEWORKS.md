# Prompt Frameworks — Index

Repo ini berisi sekumpulan **prompt framework** untuk berbagai aktivitas. Semua framework dibangun dengan filosofi yang sama:

1. **Artifact-First** — tiap stage menghasilkan dokumen yang bisa di-review.
2. **Staged & Sequential** — output stage N adalah input stage N+1.
3. **Deterministic Prompt** — prompt punya struktur baku: *Role → Context → Input → Task → Output → Constraints → Acceptance*.
4. **Traceable** — output akhir bisa dilacak balik ke niat awal.

## Daftar Framework

| Folder | Domain | Untuk siapa | Stage |
|---|---|---|---|
| [`AI SPEC FRAMEWORK/`](./AI%20SPEC%20FRAMEWORK/) | Membangun aplikasi software dari ide ke rilis | Software engineer, tech lead | 8 |
| [`AI MUSIC FRAMEWORK/`](./AI%20MUSIC%20FRAMEWORK/) | Komposisi & produksi musik (FL Studio centric) | Music producer / composer | 9 |
| [`AI OSS CONTRIBUTION FRAMEWORK/`](./AI%20OSS%20CONTRIBUTION%20FRAMEWORK/) | Modifikasi / berkontribusi ke project GitHub orang lain | Contributor / maintainer | 10 |
| [`AI RESEARCH FRAMEWORK/`](./AI%20RESEARCH%20FRAMEWORK/) | Riset akademik & publikasi (target Q1) | Peneliti AI / akademisi | 11 |
| [`AI LEARNING FRAMEWORK/`](./AI%20LEARNING%20FRAMEWORK/) | Belajar topik / skill baru | Semua | 6 |
| [`AI DEBUG FRAMEWORK/`](./AI%20DEBUG%20FRAMEWORK/) | Investigasi bug & insiden | Engineer | 7 |
| [`AI DECISION FRAMEWORK/`](./AI%20DECISION%20FRAMEWORK/) | Mengambil keputusan penting | Semua | 6 |
| [`AI WRITING FRAMEWORK/`](./AI%20WRITING%20FRAMEWORK/) | Menulis konten (artikel, dokumentasi, proposal) | Semua | 6 |

## Cara Memilih Framework

```
Mau bangun aplikasi dari nol?              → AI SPEC FRAMEWORK
Mau bikin track musik?                      → AI MUSIC FRAMEWORK
Mau kontribusi ke project orang?            → AI OSS CONTRIBUTION FRAMEWORK
Mau publish paper Q1?                       → AI RESEARCH FRAMEWORK
Mau belajar topik baru?                     → AI LEARNING FRAMEWORK
Lagi stuck debugging?                       → AI DEBUG FRAMEWORK
Bingung antara opsi A, B, C?                → AI DECISION FRAMEWORK
Mau nulis sesuatu (artikel/docs/proposal)?  → AI WRITING FRAMEWORK
```

## Konvensi Bersama

- **ID artifact:** `<KODE>-<slug-proyek>-<NNN>`. Contoh: `MB-summer-track-001`, `PB-langchain-fork-001`, `RP-attention-paper-001`.
- **Status:** `DRAFT` → `IN_REVIEW` → `APPROVED` → (opsional) `DEPRECATED`.
- **Stage skipping:** *tidak boleh*. Kalau merasa overkill, kurangi kedalaman tiap stage, jangan skip.
- **AI sebagai partner, bukan pengganti:** AI bantu drafting, eksplorasi opsi, dan kritik. Keputusan tetap di tangan Anda.

## Struktur per Framework

Tiap folder berisi:

```
<framework-name>/
├── README.md                    ← overview, prinsip, alur antar-stage
├── 01-<stage-1>.md              ← purpose + DoR/DoD + prompt + template
├── 02-<stage-2>.md
├── ...
└── examples/                    ← contoh artifact riil (opsional)
```

> Catatan: `AI SPEC FRAMEWORK/` memakai layout lama (3 file per stage: `README.md`, `prompt.md`, `artifact-template.md`). Framework lain memakai layout 1-file-per-stage karena lebih ringkas. Substansinya sama.
