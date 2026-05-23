# Stage 04 — Method Design → Method Design

**Code:** `MD` | **Output:** `MD-<paper-slug>-001`

## Purpose
Mendetilkan *apa* yang akan Anda bangun & ukur, sampai pseudo-code dan persamaan formal. Method Design adalah blueprint Section 3 paper Anda.

## DoR
- [ ] Research Proposal `APPROVED`.

## DoD
- [ ] Method Design memuat: notasi formal, deskripsi arsitektur (diagram + pseudo-code + persamaan kunci), justifikasi setiap komponen design (linked ke RQ), parameter count estimate, complexity analysis (time + memory).

---

## Prompt Template

```
1. ROLE
You are a method-spec writer. You translate ideas to formal definitions and pseudo-code.

2. CONTEXT
Saya butuh method design final.

3. INPUT
- RP-{{slug}}-001: {{paste contributions + RQs}}.
- LR-{{slug}}-001 (related method yang dipinjam/dibandingkan): {{paste}}.

4. TASK
- Tulis notasi & definisi (X, Y, model f_θ, parameter count P, dst).
- Sketsa arsitektur tingkat tinggi (block diagram → komponen).
- Pseudo-code untuk forward pass komponen baru.
- Persamaan kunci (gating, attention pattern, SSM update, dst).
- Justifikasi tiap komponen: link ke RQ/H mana.
- Complexity analysis: forward time, memory, inference vs training.
- Sebut komponen yang **identik** dengan prior work (untuk transparansi).

5. OUTPUT
04-method.md.

6. CONSTRAINTS
- Notasi konsisten (definisikan sekali, gunakan terus).
- Pseudo-code harus runnable dalam pikiran (no magic).
- Kalau pinjam dari paper lain, sitasi.

7. ACCEPTANCE
- [ ] Notasi tabel ada.
- [ ] Diagram + pseudo-code + persamaan kunci.
- [ ] Tiap komponen dijustifikasi.
- [ ] Complexity dihitung formal.
```

---

## Artifact Template — `MD-<paper-slug>-001`

```markdown
# Method Design — {{Working Title}}

| Field | Value |
|---|---|
| ID | MD-{{slug}}-001 |
| Status | DRAFT |
| Linked RP | RP-{{slug}}-001 |

## 1. Notation
| Symbol | Meaning |
|---|---|
| $x \in \mathbb{R}^{N \times d}$ | input sequence, length N, dim d |
| $h_l$ | hidden state at layer l |
| $A, B, C, D$ | SSM parameter matrices |
| $\Delta$ | step size (selectivity) |
| $W_q, W_k, W_v$ | attention projections |
| $L$ | total number of layers |
| $r$ | attention-layer ratio (1 every r layers) |

## 2. High-Level Architecture
```
[input embedding] → [Layer 1: SSM block] → [Layer 2: SSM block] → ...
                  → [Layer r: Attention block]
                  → [Layer r+1: SSM block] → ... → [output head]
```

## 3. Components

### 3.1 Selective SSM Block (adopted from Mamba [Gu&Dao, 2024])
Forward:
```
h_t = A(Δ_t) h_{t-1} + B(Δ_t) x_t
y_t = C h_t + D x_t
```
We use this as-is. Cited.

### 3.2 Sparse Attention Block (NEW: Window-Strided)
- Window: each token attends to ±W neighbors and stride-S global tokens.
- Pseudo-code:
```python
def sparse_attn(Q, K, V, window=128, stride=512):
    mask = build_window_stride_mask(N, window, stride)
    attn = softmax(Q @ K.T / sqrt(d) + mask)
    return attn @ V
```

### 3.3 Layer Interleaving (NEW)
- Pattern: every r-th layer is attention, others are SSM.
- We sweep r ∈ {2, 4, 8} in ablation.

### 3.4 Output Head
Standard LM head, untouched.

## 4. Justification (linked to RQ/H)
| Component | Why | Linked |
|---|---|---|
| Selective SSM | O(N) cost, strong long-range | H2, RQ2 |
| Sparse attention every r layers | inject global mixing for retrieval | H1, H3 |
| Sweep r | answer "how much attention is enough" | RQ1 |

## 5. Complexity
| Operation | Time | Memory |
|---|---|---|
| SSM block forward | O(N · d) | O(N · d) |
| Sparse attention (window W, stride S) | O(N · (W + N/S) · d) | O(N · (W + N/S)) |
| Total per layer | O(N · d) avg | O(N · d) |
| Inference autoregressive | O(d²) per token (SSM) | O(state size) |

## 6. Parameter Count Estimate
| Variant | Params |
|---|---|
| Hybrid-AS-S (350M) | 350M |
| Hybrid-AS-M (760M) | 760M |
| Hybrid-AS-L (1.3B) | 1.3B |

## 7. Reference Implementation Plan
- Codebase: PyTorch + flash-attn for sparse mask.
- Compatible with HF Transformers loading API.
- Mamba block: from official repo (cite, link commit).
```
