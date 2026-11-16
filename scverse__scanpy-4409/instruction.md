# Issue

**Title:** fix: respect n_top_genes with duplicate variable names

## Description

With duplicate variable names, `seurat_v3` and `seurat_v3_paper` can select more than `n_top_genes` genes because `.loc` selects every occurrence of a selected name.

Select by position instead. The regression test checks that changing gene names leaves the selected genes and statistics unchanged, across both flavors, batching, `inplace`, and `subset`.

Validation: `python -m pytest tests/test_highly_variable_genes.py -q` — 237 passed, 1 xfailed, 280 subtests passed. The new test reproduced 39 selected genes instead of 30 before the fix; all 16 cases now pass. Repository hooks pass.

**LLM usage**

- [x] LLM or coding agent used: OpenAI GPT-6 via Codex.
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line.
- [x] 
- [x] [Tests][] included.

A release note is included.

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afa0caf57144`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.