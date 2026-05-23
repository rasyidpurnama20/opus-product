# PRD + User Stories — Personal Todo App

| Field | Value |
|---|---|
| ID | `PRD-todo-001` |
| Status | `APPROVED` |
| Version | `1.0.0` |
| Linked VB | `VB-todo-001` |

## 1. Scope
MVP: tambah todo, tandai selesai, hapus todo. Single-device. Online only.

## 2. Functional Requirements
| ID | Requirement | Linked Goal |
|---|---|---|
| FR-001 | User dapat menambah todo dengan judul (1–140 char). | G1, G2 |
| FR-002 | User dapat menandai todo selesai/belum. | G1 |
| FR-003 | User dapat menghapus todo. | G1 |
| FR-004 | User melihat daftar todo miliknya, terurut terbaru di atas. | G1, G3 |

## 3. Non-Functional Requirements
| ID | Category | Requirement | Target |
|---|---|---|---|
| NFR-001 | Performance | API latency p95 | < 200 ms |
| NFR-002 | Availability | Monthly uptime | ≥ 99.5% |
| NFR-003 | Security | Auth | Bearer JWT |
| NFR-004 | Privacy | Data per user terisolasi | Strict |

## 4. Out of Scope
- Multi-user shared list.
- Sub-task / nested todo.
- Reminder & notifikasi.

## 5. Dependencies
- Auth service (existing).

## 6. Traceability
| FR/NFR | Goal |
|---|---|
| FR-001..004 | G1, G2, G3 |
| NFR-001..004 | G1, G2 |

---

## User Stories

### US-todo-001 — Tambah Todo
**As a** user, **I want** menambah todo singkat, **so that** saya tidak lupa tugas.
**Linked FR:** `FR-001`.

```gherkin
Scenario: Happy path - add todo
  Given saya sudah login
  When saya kirim POST /todos dengan title "Beli susu"
  Then respons 201 dengan body { id, title:"Beli susu", done:false }

Scenario: Edge - empty title
  Given saya sudah login
  When saya kirim POST /todos dengan title ""
  Then respons 422 dengan error code "TITLE_REQUIRED"
```

### US-todo-002 — Tandai Selesai
**As a** user, **I want** menandai todo selesai, **so that** saya tahu progres saya.
**Linked FR:** `FR-002`.

```gherkin
Scenario: Happy path - mark done
  Given saya punya todo id=T1 done=false
  When saya kirim PATCH /todos/T1 { done:true }
  Then respons 200 body.done == true

Scenario: Edge - todo not owned
  Given todo T1 milik user lain
  When saya PATCH /todos/T1
  Then respons 404
```

### US-todo-003 — Lihat Daftar
**As a** user, **I want** melihat semua todo saya, **so that** saya tahu apa yang harus dikerjakan.
**Linked FR:** `FR-004`.

```gherkin
Scenario: Happy path - list todos
  Given saya punya 3 todo
  When saya GET /todos
  Then respons 200 berisi 3 item, urut createdAt DESC

Scenario: Edge - no todo
  Given saya belum punya todo
  When saya GET /todos
  Then respons 200 dengan body []
```
