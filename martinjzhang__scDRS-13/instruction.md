# Issue

**Title:** Test cli

## Description

Changes in ./bin/scdrs
1. Updated documentation 
2. Add header and extra printing info
2. Add file check for scdrs munge-gs
3. Reformat scdrs perform-downstream --group-analysis (I haven't checked the other two)

Changes in scdrs.method:
1. Editted scdrs.method.downstream_group_analysis

Changes in scdrs.util:
1. Added function scdrs.util.str_or_list_like for determining the type of group_analysis using duck-typing (used in scdrs perform-downstream --group-analysis).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b467af5bf087`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.