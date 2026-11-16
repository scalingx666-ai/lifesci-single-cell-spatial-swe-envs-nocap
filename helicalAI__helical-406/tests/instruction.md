# Issue

**Title:** fix(security): move nosemgrep annotation onto np.load call in tahoe blocks

## Description

## Summary
Moves the trailofbits `numpy-in-pytorch-modules` nosemgrep suppression comment directly onto the `np.load(...)` line in `ChemEncoder` so it annotates the actual flagged call rather than the `torch.as_tensor(...)` wrapper.

## Details
Semgrep's line-level suppression must sit on the line containing the flagged expression. Previously the `# nosemgrep` comment preceded the `torch.as_tensor(` call, which is not the numpy operation being flagged. This change places it immediately above `np.load(drug_fps_path)`, keeping the existing explanatory comment (helicalAI/dashboard#1154) intact.

No functional change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4cb2a2e2953`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.