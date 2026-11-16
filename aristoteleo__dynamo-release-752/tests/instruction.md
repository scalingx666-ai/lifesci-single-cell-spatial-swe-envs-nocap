# Issue

**Title:** Make export_kmc robust when `kmc` is absent

## Description

Reimplements the intent of #634 (closed: stale, and the original diff had an inverted condition) on current master.

## Summary
`export_kmc` accessed `adata.uns["kmc"]` unconditionally, raising `KeyError` if no kmc object exists. Now it uses `adata.uns.get("kmc")`; when absent it logs and returns without creating `kmc_params`. Fixes the logic bug in the original #634 (which logged "empty" when kmc *existed* and would dereference `None` otherwise).

## Validation
Verified locally: calling `export_kmc` on an AnnData with no `kmc` no longer raises and creates no `kmc_params`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ecc0ccfe893`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.