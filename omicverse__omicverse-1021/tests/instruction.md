# Issue

**Title:** feat(bulk): spike-in / external-reference quantitative ChIP; pyedger robust GLM

## Description

## Summary
`ov.bulk.spikein_*`: input-corrected external-reference exposures, reference-region QC at the block level, paired / blocked designs, global-shift estimation and per-peak tests via the pyedger quasi-likelihood GLM (now with a robust dispersion option).

## Validation
- TBS diag-chipseq: 3/3 runs reward 1.
- Blind held-out task (GSE286875 ChIP-wrangler, real reads re-processed, four experiments with global loss / peak-only loss / no shift, recorded reference defects): run 1 reward 1 (5/5), no changes needed.

Companion omicos-admin PR: spikein-chip-quantification skill.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0991aaccc1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.