# Issue

**Title:** Bump biome pre-commit hook to 2.6.3

## Description

Replaces #870. Dependabot branches can't be fixed by autofix.ci, and biome 2.6.3 reformats many files (Markdown/YAML), so this lands the bump from a regular branch and lets autofix.ci push the formatting. Also updates the `biome.jsonc` schema version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba49d4ee3c89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.