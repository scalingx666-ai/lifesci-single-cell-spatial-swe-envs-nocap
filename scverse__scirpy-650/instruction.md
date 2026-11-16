# Issue

**Title:** Fix airr_mod being ignored by pl.repertoire_overlap()

## Description

Hello, I noticed that pl.repertoire_overlap() ignores the "airr_mod" keyword. 
The problem appears to be fixed by passing "params" instead of "adata" during the implicit call of tl.repertoire_overlap().

- [x] CHANGELOG.md updated
- [ ] Tests added (For bug fixes or new features)
- [ ] Tutorial updated (if necessary)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9bd88367df4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.