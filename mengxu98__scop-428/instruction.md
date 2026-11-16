# Issue

**Title:** docs: sync the RunMonocle3 use_partition default with its source

## Description

`RunMonocle3(use_partition = NULL)` resolves to `TRUE` before calling `monocle3::learn_graph()`, which itself takes `use_partition = TRUE` and never prompts, so the parameter no longer says anything about a prompt. The regenerated `man/RunMonocle3.Rd` is included.

No behaviour change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17ea7a2a13c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.