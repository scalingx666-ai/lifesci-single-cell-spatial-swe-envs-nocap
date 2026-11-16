# Issue

**Title:** fix(security): annotate CWE-502 torch.load pickle sites

## Description

## What

Resolves the two remaining `trailofbits.python.pickles-in-pytorch` (CWE-502) semgrep findings from the Bastion analysis by annotating the two `torch.load` sites and documenting why each is acceptable. **No behavior change — comment/annotation-only.**

### 1. `hyena_dna/pretrained_model.py` — false positive
Already loads with `weights_only=True` (tensor-only checkpoint; only `["state_dict"]` is used). Added the `nosemgrep` annotation and a justifying comment.

### 2. `base_models.py` — documented backward-compat fallback
The `weights_only=False` call is the `except` fallback that loads **pre-v2.0.0 full-model pickle checkpoints** (old `save_model` did `torch.save(self.model, path)`, shipped in v1.0.0–v1.12.x). It's reached only when the strict `weights_only=True` load fails. Kept for backward compatibility per decision on the issue; added `nosemgrep` plus a comment documenting the residual risk — the branch also catches corrupt/malicious files, so **only trusted checkpoints should be loaded**.

## Context

All 7 fine-tuning models inherit this `save_model`/`load_model` (none override it), and current `save_model` writes a plain state dict, so `weights_only=True` always succeeds for checkpoints produced by current code. The `weights_only=False` branch is dead for current checkpoints and lives only for v1.x backward compat.

## Testing

Comment/annotation-only; `py_compile` clean. No runtime surface changed, so existing fine-tuning save/load tests are unaffected.

Refs: helicalAI/dashboard#1154

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01QSLSjrA4gPK35MGEnfXPgJ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `740c92e4ae31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.