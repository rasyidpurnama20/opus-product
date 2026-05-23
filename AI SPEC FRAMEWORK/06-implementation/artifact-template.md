# Inline Spec Convention

Stage 06 tidak menghasilkan dokumen Markdown sebagai output utama — output utamanya adalah **source code**. Namun ada beberapa konvensi tetap ditulis di kode:

## 1. File Header

Setiap file yang berisi domain logic harus diawali dengan blok komentar:

```ts
/**
 * Module: Order Service
 * Implements: US-cart-checkout-001, US-cart-checkout-002
 * Linked spec:
 *   - PRD-cart-checkout-001 §3 FR-002
 *   - OAS:/orders [POST]
 *   - DM:Order
 * ADR: ADR-cart-checkout-001 (chosen db), ADR-cart-checkout-002 (event pattern).
 */
```

## 2. Function Header (kalau non-trivial)

```ts
/**
 * Creates an order for the current user.
 * Implements AC US-cart-checkout-001 #1, #2.
 * Throws DomainError on validation failure.
 */
export async function createOrder(input: CreateOrderInput): Promise<Order> { ... }
```

## 3. Commit Message

Format: `<type>(<area>): <subject> — T-<feature>-NNN`

Contoh:
- `feat(orders): add create order endpoint — T-cart-checkout-007`
- `test(orders): cover edge case empty cart — T-cart-checkout-013`
- `fix(orders): correct status enum casing — T-cart-checkout-019`

## 4. Pull Request Title

Format: `[T-<feature>-NNN] <Task Title>`

PR description wajib memuat:
- Linked task IDs.
- Linked user story IDs.
- Linked OAS endpoint(s).
- Acceptance criteria checklist (copy dari task).

## 5. Optional Code Spec Document

Jika selama implementasi ada keputusan kecil yang tidak cukup besar untuk ADR baru tapi penting dicatat, buat `code-spec-<feature>-001.md`:

```markdown
# Code Spec — {{Feature Name}}

| Field | Value |
|---|---|
| ID | `CS-{{feature}}-001` |
| Status | DRAFT |
| Linked Task | `T-{{feature}}-NNN` |

## Decision Log

### CS-001-1 — Use exponential backoff for retry
- Why: avoid thundering herd.
- Where: `src/services/order/retry.ts`.
- Trade-off: higher tail latency on transient errors.
```
