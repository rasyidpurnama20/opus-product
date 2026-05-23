# Stage 01 — Goal → Learning Goal

**Code:** `GO` | **Output:** `LG-<topic-slug>-001`

## Purpose
Membuat tujuan belajar yang spesifik & terukur, supaya tahu kapan "selesai".

## DoD
- [ ] LG memuat: outcome ("saya akan bisa X"), bukti ("dibuktikan dengan Y"), motivasi ("supaya saya bisa Z"), timeline, prasyarat.

## Prompt
```
ROLE: senior coach yang expert membantu orang menetapkan learning outcome.
CONTEXT: saya ingin belajar {{topik}}. Latar belakang saya: {{...}}.
INPUT: minat kasar + waktu tersedia per minggu + deadline (kalau ada).
TASK:
- Reformulasikan tujuan jadi outcome SMART ("saya bisa X dalam Y minggu, dibuktikan dengan Z").
- Identifikasi 2–3 prasyarat (pre-requisite skill).
- Bedakan "knowing" vs "doing": fokus ke "doing".
- Sarankan capstone outcome (project apa di akhir).
OUTPUT: 01-learning-goal.md mengikuti template.
CONSTRAINTS: tidak boleh "saya ingin tahu tentang X" — harus "saya bisa lakukan X".
ACCEPTANCE: outcome SMART, capstone defined, prereq listed.
```

## Template
```markdown
# Learning Goal — {{Topic}}

| Field | Value |
|---|---|
| ID | LG-{{slug}}-001 |
| Status | APPROVED |
| Date | {{...}} |

## Outcome (SMART)
"Saya bisa {{verb}} {{object}} {{condition}} dalam {{N}} minggu, dibuktikan dengan {{evidence}}."

Contoh: "Saya bisa membangun pipeline DSP real-time di Rust untuk audio plugin VST3 dalam 12 minggu, dibuktikan dengan 1 plugin reverb berfungsi yang dirilis di GitHub."

## Motivation (Why)
{{Mengapa skill ini penting bagi saya — karir, project, curiosity, masalah konkret yang saya hadapi.}}

## Prerequisites
- {{prereq 1}} — sudah ada / belum ada (rencana belajar dulu).
- {{prereq 2}}.

## Capstone Outcome
{{Project / karya / sertifikasi yang akan dihasilkan di akhir.}}

## Timeline
- Total: {{N}} minggu.
- Per minggu: {{N}} jam.
- Deadline: {{date}}.

## Anti-Goals (NOT learning)
- {{hal yang sengaja tidak dipelajari sekarang}}.
```
