# Data Model + API + UI Spec — Personal Todo App

| Field | Value |
|---|---|
| ID | `DM-todo-001` (digabung DM+OAS+UIS untuk contoh) |
| Status | `APPROVED` |
| Linked ARCH | `ARCH-todo-001` |

## Data Model

### `todos`
| Attribute | Type | Constraint |
|---|---|---|
| id | UUID v7 | PK |
| user_id | UUID v7 | NOT NULL, FK logical (Auth Service) |
| title | VARCHAR(140) | NOT NULL |
| done | BOOLEAN | NOT NULL DEFAULT false |
| created_at | TIMESTAMPTZ | NOT NULL DEFAULT NOW() |
| updated_at | TIMESTAMPTZ | NOT NULL DEFAULT NOW() |

### Indexes
| Index | Reason |
|---|---|
| `(user_id, created_at DESC)` | Listing per user, urut terbaru |

---

## OpenAPI (subset)

```yaml
openapi: 3.1.0
info:
  title: Todo API
  version: 1.0.0
servers: [{ url: https://api.example.com/v1 }]
security: [{ bearerAuth: [] }]
paths:
  /todos:
    get:
      summary: List todos for current user
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: array
                items: { $ref: '#/components/schemas/Todo' }
    post:
      summary: Create a todo
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required: [title]
              properties:
                title: { type: string, minLength: 1, maxLength: 140 }
      responses:
        '201':
          description: Created
          content:
            application/json:
              schema: { $ref: '#/components/schemas/Todo' }
        '422':
          description: Validation error
  /todos/{id}:
    patch:
      summary: Update todo (toggle done)
      parameters:
        - in: path
          name: id
          required: true
          schema: { type: string, format: uuid }
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                done: { type: boolean }
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema: { $ref: '#/components/schemas/Todo' }
        '404': { description: Not found / not owned }
    delete:
      summary: Delete todo
      parameters:
        - in: path
          name: id
          required: true
          schema: { type: string, format: uuid }
      responses:
        '204': { description: Deleted }
        '404': { description: Not found / not owned }
components:
  securitySchemes:
    bearerAuth: { type: http, scheme: bearer, bearerFormat: JWT }
  schemas:
    Todo:
      type: object
      required: [id, title, done, createdAt]
      properties:
        id: { type: string, format: uuid }
        title: { type: string }
        done: { type: boolean }
        createdAt: { type: string, format: date-time }
```

---

## UI Spec (subset)

### Screen S1 — `TodoListScreen`
- **Linked US:** `US-todo-001`, `US-todo-002`, `US-todo-003`.
- **Data:** `GET /todos`, `POST /todos`, `PATCH /todos/{id}`, `DELETE /todos/{id}`.

**Components**
- Input "Tambah todo…" + tombol Add.
- List item: checkbox, title, tombol delete.

**States**
| State | Trigger | UI |
|---|---|---|
| Loading | initial fetch | Skeleton 3 baris |
| Empty | array kosong | Illustrasi "Belum ada todo" + CTA fokus ke input |
| Error | network/5xx | Banner merah + Retry |
| Success | data | Render list |

**Inline validation**
- Title kosong → tombol Add disabled, helper text "Tulis dulu yuk."
- Title > 140 char → counter merah, tombol Add disabled.
