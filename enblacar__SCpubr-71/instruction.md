# Issue

**Title:** Fix for do_VolcanoPlot when order_tags_by = "both"

## Description

. Changed object references when creating 'data.label' for the "both" condition. Added calls to bind_rows for the "pvalue" and "logfc" conditions so that 'data.label' is created.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af2828dbfce7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.