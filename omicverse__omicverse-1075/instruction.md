# Issue

**Title:** ov.datasets.cite_seq loader + ov.vi tutorial helpers

## Description

- `ov.datasets.cite_seq()`: real loader for 10x PBMC 5k+10k CITE-seq (same files as scvi-tools' pbmcs_10x_cite_seq, without scvi-tools): 10,849 cells × 15,792 genes, 14 proteins in `obsm['protein_expression']`, `batch` column; `protein_join='outer'` → 29 proteins.
- `ov.vi.plot_history`, `ov.vi.integration_metrics` (scib-metrics), `ov.vi.MemoryMonitor` used by the tutorials.
- Tests: tests/test_datasets_cite_seq.py (network test gated by OV_TEST_NETWORK=1), tests/vi/test_utils.py.

Tutorials:

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab9e677314f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.