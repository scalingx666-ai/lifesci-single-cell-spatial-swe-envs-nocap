# Issue

**Title:** build: migrate to torch 2.10 / CUDA 13 / Python 3.12 (v3.0.0)

## Description

Part of the torch 2.10 / CUDA 13 / Python 3.12 migration (helical-version-set umbrella).

**Targets `main`.** This supersedes #389 (which was opened against `release`) which run all the integration test successfully (the notebook failed by it is fixed in the current commits in here)

### Version: `3.0.0` (major bump)

This release drops previously supported runtimes, which is backward-incompatible under SemVer and warrants a **major** bump (not patch/minor):

- `requires-python` `>=3.11` → `>=3.12` — Python 3.11 support dropped
- `torch==2.7.0` → `torch==2.10.0` (pinned exact) — forces a core shared-runtime bump
- CUDA 12 → CUDA 13 (cu13 wheels for torch/mamba/causal-conv1d/flash-attn) — drops CUDA 12 GPUs / drivers `<580`
- removed dependencies: `loompy`, `scib`, `louvain`, `gitpython`

Existing users on Python 3.11 or CUDA 12 cannot upgrade in place.

On the reasoning of why the upgrade was done to 3.12, cuda13 and pytorch 10, check below report

### Changes

- `Dockerfile`: base image → `pytorch/pytorch:2.10.0-cuda13.0-cudnn9-runtime`
- `pyproject.toml`: `torch==2.10.0` via the cu130 index (`[[tool.uv.index]]` + `[tool.uv.sources]`), `requires-python >=3.12`, mamba-ssm/causal-conv1d bumped to cu13 wheels, drop loompy/scib/louvain/gitpython, protobuf floor → `constraint-dependencies`, add `pypi.nvidia.com` index, add explicitly-imported deps (`scanpy`, `requests-cache`, `torchmetrics`, `catalogue`).
- `pyproject.toml` (dev extra): bump `pytest` 8.2.0 → 9.0.3, `pytest-cov` 5.0.0 → 7.1.0, `pytest-mock` 3.14.0 → 3.15.1 for the Python 3.12 stack.

### Notebook fix: HyenaDNA dataset loading (`datasets` 3.x)

The migration bumps `datasets` from 2.14.7 to 3.6.0, which broke the `notebooks` CI job — `Hyena-DNA-Inference.ipynb` and `HyenaDNA-Fine-Tuning.ipynb` failed with:

```
ValueError: BuilderConfig 'promoter_tata' not found. Available: ['default']
```

**Why:** The `InstaDeepAI/nucleotide_transformer_downstream_tasks_revised` dataset used to ship a custom Python loading script that defined one `BuilderConfig` per task (`promoter_tata`, `enhancers`, …), which `datasets` 2.14.7 executed automatically. The dataset has since been restructured into plain parquet files organized one directory per task, and it declares **no named configs**. In `datasets` 3.x the remote-script path is no longer taken by default, so the old positional-config call `load_dataset(repo, "promoter_tata")` can no longer resolve the subset and only sees the auto-inferred `'default'` config.

**Fix:** Select the task via `data_dir=label` instead of the config name. Verified against `datasets==3.6.0` that this loads the correct `promoter_tata` splits (train 5062 / test 212) with the same `sequence`/`label` columns the downstream cells rely on. The inference notebook also now prints `label` instead of `.config_name` (which is `"default"` under the new layout).

Validated end-to-end via a CPU + full GPU image build (torch `2.10.0+cu130`, flash-attn/mamba/causal-conv1d forward passes on GPU).

## Version-selection rationale (full report)

<details>
<summary>Why torch 2.10 / CUDA 13 / Python 3.12 — click to expand</summary>

# Why torch 2.10 / CUDA 13 / Python 3.12 — Version-Selection Rationale


---

## 1. Executive summary

AWS ECR image scanning (Inspector) flagged our container images for shipping an
**outdated, vulnerable PyTorch (2.7.0)**. We are remediating by upgrading the whole
stack in lock-step:

| Component   | Current (flagged)      | Selected (new)          |
|-------------|------------------------|-------------------------|
| Python      | 3.11 (cp311)           | **3.12 (cp312)**        |
| PyTorch     | 2.7.0                  | **2.10.0**              |
| CUDA        | 12.x (cu12)            | **13.0 (cu13)**         |
| mamba-ssm   | 2.2.5                  | 2.3.2.post1             |
| causal-conv1d | 1.5.1                | 1.6.2.post1             |
| flash-attn  | 2.7.4.post1            | 2.8.3                   |

**The one-sentence version:** We move to **torch 2.10** because it is the only
release that patches the high-severity PyTorch advisory affecting every version
we could otherwise ship (CVE-2026-24747, CVSS 8.8). The moment we commit to
torch 2.10, our three GPU-compiled dependencies — and **flash-attention in
particular** — only publish prebuilt binaries for **CUDA 13 + Python 3.12**, so
those two choices are *forced*, not preferences.

We do **not** build these CUDA extensions from source. We rely on the
upstream-published **precompiled wheels**; building from source in CI is slow,
fragile, and unsupported by these projects for arbitrary combinations. So the
available prebuilt-wheel matrix is the hard constraint that dictates the stack.

---

## 2. The three CUDA-compiled dependencies

All three ship as **version-specific precompiled wheels** tagged
`+cu{CUDA}torch{TORCH}...cp{PY}-linux_x86_64`. A wheel only exists for the exact
`(CUDA, torch, Python)` triple it was built against.

1. **mamba-ssm** — `state-spaces/mamba` (Mamba SSM kernels)
2. **causal-conv1d** — `Dao-AILab/causal-conv1d` (the causal conv kernel mamba needs)
3. **flash-attention** (`flash-attn`) — `Dao-AILab/flash-attention`

(The "another one whose name differs a bit" is **causal-conv1d**.)

---

## 3. Prebuilt-wheel availability for torch > 2.7 (linux_x86_64)

Enumerated directly from each project's GitHub release assets on 2026-07-13,
restricted to torch ≥ 2.8 and the **latest** wheel line of each library.

### Per-library support matrix

Legend: ✅ = prebuilt wheel exists · ❌ = none published

| Library (latest line)        | torch | cu12 | cu13 | cp310 | cp311 | cp312 | cp313 |
|------------------------------|:-----:|:----:|:----:|:-----:|:-----:|:-----:|:-----:|
| **mamba-ssm** 2.3.2.post1    | 2.8   | ✅   | ❌   | ✅    | ✅    | ✅    | ✅    |
|                              | 2.9   | ✅   | ✅   | ✅    | ✅    | ✅    | ✅    |
|                              | 2.10  | ✅   | ✅   | ✅    | ✅    | ✅    | ✅    |
| **causal-conv1d** 1.6.2.post1| 2.8   | ✅   | ❌   | ✅    | ✅    | ✅    | ✅    |
|                              | 2.9   | ✅   | ✅   | ✅    | ✅    | ✅    | ✅    |
|                              | 2.10  | ✅   | ✅   | ✅    | ✅    | ✅    | ✅    |
| **flash-attn** 2.8.3         | 2.8   | ✅   | ❌   | ✅    | ✅    | ✅    | ✅    |
|                              | 2.9   | ✅   | ✅   | ❌    | ❌    | ✅    | ❌    |
|                              | 2.10  | ❌   | ✅   | ❌    | ❌    | ✅    | ❌    |

**flash-attention is the bottleneck.** Its current release (2.8.3) publishes a
torch 2.10 wheel **only** for `cu13` + `cp312`. It has already dropped cu12 and
every Python version except 3.12 for torch 2.10. mamba-ssm and causal-conv1d are
far more flexible (all of cp310–cp313, cu12 **and** cu13) and simply follow
whatever flash-attention forces.

### Intersection — combos where ALL THREE libraries have a prebuilt wheel

This is the only thing that actually matters: what can we install together?

| torch | Feasible (CUDA, Python) combos, x86_64            | Notes |
|:-----:|---------------------------------------------------|-------|
| 2.8   | **cu12** × {cp310, cp311, cp312, cp313}           | cu13 not built for torch 2.8 by any of the three |
| 2.9   | {cu12, cu13} × **cp312 only**                     | flash-attn caps Python to 3.12 |
| 2.10  | **cu13 × cp312 only**                             | flash-attn 2.8.3 is cu13+cp312 only → this is our target |

> Note: flash-attn **2.8.1** (older) offered torch 2.10 on cu12/cu13 × cp312/cp313.
> We chose **2.8.3** (current stable) — it narrows torch 2.10 to **cu13 + cp312**.
> Staying on the latest patch line is the safer default, and it collapses the
> matrix to a single supported combination, which removes ambiguity.

**Conclusion:** For torch 2.10, `cu13 + cp312 + linux_x86_64` is the *only*
triple with a complete prebuilt-wheel set across all three libraries. CUDA 13
and Python 3.12 are therefore not independent decisions — they are entailed by
choosing torch 2.10.

---

## 4. Why torch 2.10 (and not 2.8 or 2.9)

The upgrade is security-driven, so the deciding factor is CVE coverage.

- **CVE-2026-24747** (official PyTorch GitHub Security Advisory
  `GHSA-63cw-57p8-fm3p`, **CVSS 8.8 High**) — memory-corruption / potential RCE
  in the `torch.load(..., weights_only=True)` unpickler. **Affects every release
  from 2.6.0 through 2.9.x — including our current 2.7.0 — and is fixed only in
  2.10.0.** This is the single most important, vendor-confirmed reason.
- torch **2.8** and **2.9** would *not* clear this advisory. Only **2.10.0** does.
- torch **2.11 / 2.12** are not viable: at time of writing they have **no
  prebuilt accelerator (mamba/causal/flash) wheels at all**, and torch 2.12 has
  no CUDA wheels published. 2.10 is the newest torch our GPU stack can run on.

So 2.10 is the *floor* that fixes the high-severity CVE and the *ceiling* that
our compiled dependencies support — it is the only option.

---

## 5. CVEs per PyTorch version

Counts reflect what an enriched scanner (AWS Inspector uses NVD + GitHub Advisory
Database) would report for the `torch` package, as of 2026-07-13. The landscape
has two tiers: **officially reviewed PyTorch advisories** (high confidence) and a
large set of **2025 VulDB-sourced** correctness/DoS/memory entries (many disputed,
unreviewed, or with no fixed version). Both tiers are shown because AWS ingests both.

| torch version | Approx. total scanner findings | Severity split | High-sev `weights_only` RCE (CVE-2026-24747) |
|:-------------:|:------------------------------:|----------------|:--------------------------------------------:|
| **2.7.0** (current) | **≈ 18–19** | 3 High / ~11 Med / ~5 Low | ❌ **Vulnerable** |
| 2.8.0         | ≈ 14–16 | still incl. the 8.8 High | ❌ Vulnerable |
| 2.9.0         | ≈ 8–10  | still incl. the 8.8 High | ❌ Vulnerable |
| **2.10.0** (selected) | **≈ 6–7** | 0–1 High (see below) / rest Med | ✅ **Fixed** |

**What the upgrade from 2.7.0 → 2.10.0 clears** (every CVE with a confirmed fix ≤ 2.10):
CVE-2026-24747 (8.8 High), CVE-2025-3001, CVE-2025-2999, CVE-2025-55551/55552,
CVE-2025-3730, CVE-2025-46148, CVE-2025-55553/55557/55558/55560, CVE-2025-2953.
→ roughly a **60%+ reduction in findings** and, critically, elimination of the
only high-severity, vendor-confirmed advisory.

**Residual on 2.10.0 (honest caveat):** a handful of findings remain, mostly
2025 VulDB entries with no reliable fixed-version metadata or disputed/overly-broad
version ranges (e.g. CVE-2025-3000, -3121, -3136, -4287, -55554). One NVD entry,
**CVE-2026-4538** (`.pt2` pickle fallback), currently names 2.10.0 with no
published fix — but it is **unreviewed (VulDB-sourced), the upstream fix PR was
closed unmerged, and it is not a vendor-confirmed PyTorch advisory.** No shipping
torch release is free of it, so it is not a reason to prefer any other version.
Standard mitigation applies regardless of version: **do not load untrusted
`.pt`/`.pth`/`.pt2`/TorchScript checkpoints.**

---

## 6. Bottom line for leadership

1. **Security forced the move.** Our images ran torch 2.7.0, which AWS flags and
   which carries a **CVSS 8.8 High** PyTorch advisory (CVE-2026-24747). Only
   **torch 2.10.0** patches it; 2.8 and 2.9 do not.
2. **The GPU libraries forced the rest.** We install upstream **precompiled**
   mamba-ssm, causal-conv1d, and flash-attention wheels (we don't build from
   source). For torch 2.10, the only `(CUDA, Python)` combination with a complete
   prebuilt-wheel set across all three is **CUDA 13 + Python 3.12** —
   flash-attention publishes nothing else. CUDA 13 and Python 3.12 are
   *consequences* of choosing torch 2.10, not separate bets.
3. **Net result:** newest supportable, actively-maintained stack; the flagged
   high-severity CVE eliminated; roughly a 60% cut in total scanner findings.

*(GPU-driver readiness note: CUDA 13 requires NVIDIA driver ≥ R580. AWS GPU nodes
are ready — pinned Bottlerocket NVIDIA AMI ≥ v1.54.0 ships driver 580.126.09. The
on-prem V1 box (570.211.01) needs a driver upgrade before it can run the cu13 image.)*

</details>

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01CpgHKFsoeKfqrmrFdvESX4

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fbb1264b420`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.