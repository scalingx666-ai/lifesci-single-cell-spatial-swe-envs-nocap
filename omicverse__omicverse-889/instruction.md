# Issue

**Title:** perf(pp): GPU/torch sccomposite post-processing (fixes 1e5-cell OOM)

## Description

sccomposite's per-cell post-processing (`prob_k0_rna` / `reliability_rna` / `log_joint_one_k_rna`) pulled the fitted model back to **CPU** and used scipy `gamma.pdf` + **float128** + a dense **`(n_cells × n_genes × k)`** array — the 3-D array **OOM'd at ~1e5 cells** and float128 is software-emulated.

Rewritten in **pure torch on the model's device (GPU when available)**: torch gamma/poisson log-densities + `torch.logsumexp`, and `reliability_rna` reduces the `k` mixture terms with an **incremental log-sum-exp** so the 3-D array is never allocated.

**Bit-consistent** with the old scipy path — prob_k0 atol 1e-8, consistency + doublet calls + outlier flags identical (`tests/pp/test_sccomposite_torch_postproc.py`). `rna_fit_goodness` (a grid-indexed goodness scalar that doesn't scale with cells) is left on scipy.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `950f288cf234`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.