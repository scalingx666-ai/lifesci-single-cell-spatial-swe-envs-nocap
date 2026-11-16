# Issue

**Title:** README: runtime and peak-memory comparison on SEA-AD (1.4M cells)

## Description

Adds a two-panel figure (total runtime | peak memory) to the Introduction: omicverse 2.4.2 (storage='disk', 64 threads) vs brisc (64 threads) measured on the same AMD EPYC 9754 node, and Scanpy / Seurat + BPCells as reported in the brisc paper (192-core node). Footnote and text state the hardware difference and the embedding used.

Figure script: omicverse/anndataoom-fast benchmarks/fig4/plot_headline.py.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `901380fa46a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.