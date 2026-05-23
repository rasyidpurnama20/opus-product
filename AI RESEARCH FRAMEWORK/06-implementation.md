# Stage 06 — Implementation → Reproducible Codebase

**Code:** `IM` | **Output:** `RC-<paper-slug>-001` (link ke repo)

## Purpose
Membangun codebase yang **reproducible**, terorganisir, dan dapat di-rilis bersamaan dengan paper. Banyak penolakan paper Q1 dipicu masalah reproducibility yang ketahuan saat reviewer mencoba menjalankan.

## DoR
- [ ] Experiment Plan `APPROVED`.

## DoD
- [ ] Repo punya: README jelas, env spec (conda/pyproject + lockfile), `train.py` + `eval.py`, config-driven (YAML/Hydra), seed reproducible, checkpoint loader, Dockerfile / Apptainer (opsional tapi disarankan).
- [ ] Reproducibility test: clone fresh → `make reproduce-headline` jalan tanpa error.
- [ ] Pre-registered seed list.

---

## Prompt Template

```
1. ROLE
You are an MLOps engineer for research labs. Reproducibility is your obsession.

2. CONTEXT
Saya akan implement EP-{{slug}}.

3. INPUT
- EP-{{slug}}-001: {{paste}}
- Existing scaffold (jika ada): {{...}}.

4. TASK
- Sketsa repo layout: src/, configs/, scripts/, results/, tests/.
- Spek environment: pyproject.toml + lockfile, exact CUDA + framework.
- Sketsa train.py + eval.py (config-driven).
- Pseudo-code seed control: numpy, torch, cuda, dataloader.
- Dockerfile minimal.
- Hash data + config bersama checkpoint.

5. OUTPUT
06-codebase-spec.md (lalu eksekusi di repo eksperimen).

6. CONSTRAINTS
- Determinism: cuDNN deterministic mode dibahas (trade-off latency vs reprod).
- Logging: wandb/mlflow + local fallback.

7. ACCEPTANCE
- [ ] `make reproduce-headline` documented.
- [ ] Env spec dengan lockfile.
- [ ] Seed control eksplisit.
- [ ] Data versioning (DVC / HF dataset version) dipertimbangkan.
```

---

## Artifact Template — `RC-<paper-slug>-001`

```markdown
# Reproducible Codebase Spec — {{Working Title}}

| Field | Value |
|---|---|
| ID | RC-{{slug}}-001 |
| Repo | https://github.com/{{me}}/{{slug}} |
| Linked EP | EP-{{slug}}-001 |

## 1. Layout
```
{{slug}}/
├── README.md             ← reproduce in 60s
├── pyproject.toml        ← dep + tool config
├── uv.lock               ← reproducible install
├── Dockerfile
├── Makefile              ← reproduce-headline, reproduce-ablation, eval-only
├── configs/
│   ├── base.yaml
│   ├── exp/
│   │   ├── headline.yaml
│   │   └── ablation/
│   └── data/
├── src/{{slug}}/
│   ├── data/
│   ├── models/
│   ├── train.py
│   ├── eval.py
│   ├── seed.py
│   └── utils/
├── scripts/
│   ├── download_data.sh
│   ├── reproduce_headline.sh
│   └── reproduce_ablation.sh
├── tests/
│   ├── unit/
│   └── repro/             ← tiny repro tests (1 step, 1 seed)
└── results/               ← (gitignored) output csv/json/logs
```

## 2. Environment
- Python 3.11.
- CUDA 12.1, PyTorch 2.4.1.
- All deps via `uv` with lockfile committed.
- `Dockerfile` based on `nvidia/cuda:12.1.1-cudnn8-devel-ubuntu22.04`.

## 3. Seed Control
```python
def set_seed(seed: int, deterministic: bool = True):
    random.seed(seed)
    np.random.seed(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)
    if deterministic:
        torch.backends.cudnn.deterministic = True
        torch.backends.cudnn.benchmark = False
        os.environ["CUBLAS_WORKSPACE_CONFIG"] = ":4096:8"
        torch.use_deterministic_algorithms(True, warn_only=True)
```
Trade-off: deterministic ~10% slower; documented.

## 4. Config-Driven
- Hydra / OmegaConf.
- One YAML per experiment.
- `python -m {{slug}}.train --config configs/exp/headline.yaml seed=0`.

## 5. Reproduce Headline
```bash
make repro-deps        # install env from lockfile
make download-data     # downloads + verifies sha256
make reproduce-headline # 5 seeds × main config
# outputs results/headline-{model}-{seed}.json
make headline-table    # aggregates into mean ± std
```

## 6. Logging
- W&B project: `{{slug}}-runs`.
- Local fallback: `results/<run-id>/{train.log,metrics.csv,config.yaml,git.txt}`.
- `git.txt` records commit hash + dirty status.

## 7. Data Versioning
- Datasets pinned by sha256 (or HF dataset version).
- Download scripts verify checksum.
- For private data, document procedure separately (no dump in repo).

## 8. Checkpoints
- Format: `state_dict + optimizer + scheduler + step + config + git_sha`.
- Saved every 5k steps.
- Best-on-val saved separately.

## 9. Repro-Test (tiny)
A 5-minute pipeline that runs end-to-end on 1 GPU, asserts loss < threshold after 100 steps. Runs in CI.

## 10. Release Plan (with paper)
- Public release on day of paper acceptance / arXiv post.
- Include: code, configs, eval scripts, model checkpoints (HF Hub), data download script, Dockerfile.
- Reproducibility statement section in paper points to this repo + commit hash.
```
