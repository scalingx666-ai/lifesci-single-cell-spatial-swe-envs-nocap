# Issue

**Title:** feat(pl): add radial cell annotation tree

## Description

Add `ov.pl.celltype_tree()` to draw a radial annotation tree from AnnData or a summary table. AnnData input groups cells by the full annotation path, adds cell proportions, and averages selected genes or numeric observation columns. Each track uses its own values and can be standardized across leaves.

Validated with 19 plotting tests, including sparse expression, layers, raw expression, and nullable tracks. The bilingual tutorials render a 19-cluster Paul15 example and a 73-subtype CIMA example.

Merge the  first so the tutorial commit is available on the documentation branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0991aaccc1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.