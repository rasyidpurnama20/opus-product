# Stage 06 — Implementation

**Code:** `IMP`
**Output Artifact:** Source Code (`SRC`) + Inline Spec (header komentar)

## Tujuan
Mengubah artifact upstream menjadi kode yang berjalan. Stage ini adalah satu-satunya stage di mana AI menulis kode dalam jumlah besar — dan **hanya** boleh dilakukan jika artifact upstream `APPROVED`.

## Owner
Engineer + AI. Engineer bertanggung jawab atas hasil akhir.

## Input
- `TB-<feature>` — task per task dieksekusi.
- `DM`, `OAS`, `UIS` sebagai kontrak.
- `ARCH` + ADR sebagai pagar pembatas teknologi.

## Output
- Source code (commit per task).
- **Inline Spec**: setiap modul/file/fungsi non-trivial punya header komentar yang merujuk artifact:
  ```ts
  /**
   * Implements US-auth-003, FR-002.
   * See OAS:/auth/login (POST), DM:User.
   */
  ```
- (Opsional) `code-spec-<feature>-001.md` jika ada keputusan implementasi yang tidak tercover ADR.

## DoR
- [ ] Task dari `TB` punya status `READY`.
- [ ] Semua artifact upstream `APPROVED`.

## DoD
- [ ] Semua acceptance criteria task tercentang.
- [ ] Linter & type-checker pass.
- [ ] Unit test untuk logic non-trivial ada (kalau project punya budaya test).
- [ ] Inline spec menyebut artifact ID yang dipenuhi.
- [ ] Pull request mereferensikan task `T-<feature>-NNN` di judul.

## Anti-Pattern
- Menulis kode tanpa task (`T-`) atau tanpa user story.
- Menambah dependensi baru tanpa ADR.
- "Refactor besar-besaran" digabung di PR fitur.
