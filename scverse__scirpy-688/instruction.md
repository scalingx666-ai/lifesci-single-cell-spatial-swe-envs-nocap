# Issue

**Title:** drop distance_key from ir.tl.define_clusters

## Description

- drop distance_key from input parameters
- drop distance_key from clause to potentially rerun ir.pp.ir_dist
- add unsilensing via logging warn for distance_key replacement.
- drop distance_key from kwargs if present
- pass distance key explicitly



- [ ] CHANGELOG.md updated
- [ ] Tests added (For bug fixes or new features)
- [ ] Tutorial updated (if necessary)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64da65fbde8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.