# Issue

**Title:** {ts} documentation update

## Description

When filtering against a whitelist with `extract`, no longer need to supply `--filter-cell-barcode` and `--whitelist`, just the later. Note that former option remains but is hidden from user in `--help` text and will raise an `U.info` to inform the user this option is no longer required.  for motivation

Also adding a specific doc page to walk through the network-based deduplication. This is following an email conversation with a user who pointed out some inadequacies/inconsistencies in the way the methods were described across the original CGAT blog post/GR publication/command-line documentation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3251182d9a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.