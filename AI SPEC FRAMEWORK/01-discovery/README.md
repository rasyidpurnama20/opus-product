# Stage 01 — Discovery

**Code:** `DSC`
**Output Artifact:** Vision Brief (`VB`)

## Tujuan
Mendefinisikan *masalah* dan *peluang* dari fitur/produk sebelum membicarakan solusi. Ini adalah satu-satunya stage di mana solusi teknis belum boleh dibahas.

## Owner
Product Manager / Founder / Domain Expert. AI berperan sebagai *facilitator & writer*.

## Input
- Ide kasar dari stakeholder (transkrip wawancara, voice note, brief lisan).
- Data pendukung opsional: hasil riset user, analitik, kompetitor.

## Output
- `vb-<feature>-<nnn>.md` — **Vision Brief** mengikuti `artifact-template.md`.

## Definition of Ready (DoR)
- [ ] Ada problem statement awal dari stakeholder.
- [ ] Diketahui setidaknya satu segmen user.

## Definition of Done (DoD)
- [ ] Vision Brief berisi: Problem, Target User, Goals, Non-Goals, Success Metrics.
- [ ] Tidak menyebut teknologi/implementasi spesifik.
- [ ] Setiap goal punya metric terukur.
- [ ] Disetujui oleh stakeholder bisnis (status `APPROVED`).

## Anti-Pattern
- Loncat ke "kita pakai React + Postgres".
- Goals tanpa metrik (mis. "user senang").
- Tidak ada non-goals → scope creep.
