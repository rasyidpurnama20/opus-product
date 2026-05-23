# Stage 04 — Edit → Edit Pass

**Code:** `ED` | **Output:** `EP-<piece-slug>-001`

## Purpose
**Structural edit**: cek argumen, struktur, klaritas. Bukan typo (itu polish). 

## DoD
- [ ] Struktur konsisten dengan outline.
- [ ] Tiap claim punya bukti / contoh.
- [ ] Tidak ada section yang "tidak punya tujuan jelas".
- [ ] Word count di range target.

## Prompt
```
ROLE: structural editor.
INPUT: FD-{{slug}}-001 + AB + OL.
TASK:
- Pass 1 (struktur): tiap section punya tujuan? Section bisa diurut ulang lebih jelas?
- Pass 2 (argumen): tiap claim punya bukti? Ada gap logika?
- Pass 3 (klaritas): kalimat panjang yang bisa dipendekkan, jargon yang perlu dijelaskan.
- Pass 4 (audience fit): apakah persona AB akan ngerti & care?
- Sarankan cuts (paragraf yang tidak menambah).
OUTPUT: 04-edit-notes.md (notes) + revisi inline di draft.
CONSTRAINTS: tidak typo-check di stage ini.
ACCEPTANCE: 4 pass dilakukan, ada cut suggestions, ada gap logika diidentifikasi.
```

## Template — Edit Pass Notes
```markdown
# Edit Notes — {{Piece Title}}

| Field | Value |
|---|---|
| ID | EP-{{slug}}-001 |
| Linked FD | FD-{{slug}}-001 |
| Pass | 1/4: structural |

## Structural
- S5 (Migration Strategy) terasa terpotong dari S4 — pindah ke setelah S2 supaya alur "problem → why gather fail → fix → migration → mental model" lebih intuitif? **Decision:** keep order, tapi tambahkan transition paragraph 1 baris di awal S5.
- S4 dan S5 panjangnya tidak balance — S4 terlalu lama untuk ide yang bisa dijelaskan dalam 1 diagram.

## Argument
- Claim "task group eliminates entire class of bug" — perlu lebih spesifik di S3. Tambah 2 contoh konkret.
- Claim "gather is not enough" — bukti baik, tapi anchor ke 1 study/post resmi (cite).

## Clarity
- Paragraf 3 di S2: kalimat 47 kata, pecah jadi 2.
- Jargon "structured concurrency" — definisi singkat di S1 (1 baris), di S3 elaborasi.

## Audience Fit
- Persona = mid-level Python dev. Saat ini draft asumsi sudah tahu nursery — terlalu maju.
  - Tambah 2 baris di S3: "kalau belum familiar dengan trio's nursery, anggap dia 'with-block yang otomatis tunggu semua child task selesai'."

## Cuts (suggested)
- Paragraf 2 di S4 (filosofi) bisa dipotong → tidak menambah pemahaman teknis.
- 1 code example duplikat di S3 vs S5.

## Word Count
- Current: 1730 (target 1500).
- Cuts above bring to ~1520.

## Next
- Apply edits → produce v2.
- Then move to polish stage.
```
