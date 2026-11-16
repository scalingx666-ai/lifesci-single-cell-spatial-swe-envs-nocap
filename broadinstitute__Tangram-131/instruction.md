# Issue

**Title:** Added refinements

## Description

We have developed several refinements aimed at improving consistency and certainty across multiple training runs. This includes (1) gene selection, (2) regularization, (3) incorporation of neighborhood information, and (4) cell selection. More details can be found in our preprint: https://www.biorxiv.org/content/10.1101/2025.01.27.634996v1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d537ff936a1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.