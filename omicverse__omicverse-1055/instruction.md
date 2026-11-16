# Issue

**Title:** README: benchmark figure with CPU/GPU groups

## Description

Adds Seurat v6 (our run: 6.0.0 in-memory, setThreads(64); RunUMAP segfaulted after 7.8 h) to the CPU group, and a GPU group: omicverse[gpu] / omicverse[mixed] on one H100 and rapids-singlecell from the brisc paper (4x H100).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fbbb7e3b0a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.