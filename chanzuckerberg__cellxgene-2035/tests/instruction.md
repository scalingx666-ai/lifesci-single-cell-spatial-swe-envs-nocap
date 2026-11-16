# Issue

**Title:** Fix deprecated np.unicode type

## Description

Until numpy version 1.20.0, `numpy.unicode` was an alias for `str` in python3. In 1.20.0, it's fully deprecated and is an `int`. This is bad and breaks things. This commit drops the `np.unicode` alias and just uses `str`, as is advised here:
https://numpy.org/devdocs/release/1.20.0-notes.html#deprecations

#### Reviewers
@MDunitz

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90a4ff75268e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.