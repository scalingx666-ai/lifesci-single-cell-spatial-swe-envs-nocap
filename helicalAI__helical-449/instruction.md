# Issue

**Title:** fix(geneformer): keep var["ensembl_id"] when sum_ensembl_ids collapses genes

## Description

Replicates #434 by @mircomacchi so CI can run. Fork PRs cannot use our self-hosted runner. The commit is cherry-picked unchanged, with Mirco as author.

.

`sc.concat` keeps only the var columns that both parts share. So when `sum_ensembl_ids` collapses genes, the result loses `ensembl_id`. `tokenize_anndata` then raises `KeyError`. The fix restores the column from the collapsed `var_names`. A new test checks the column, its values and the summed counts.

Please merge with a merge commit, not squash, to keep the original author.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0935648fb7fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.