# Issue

**Title:** Multiselect sort fixed

## Description

This PR fixes the reported bug, i.e., when the last strategy is selected in case of multi-select featurelist, the legend /scatterplot view should show the last (most recent) selected gene, rather than alphabetic sorted gene from the list.
It also provides the featureAggregateStrategy option in the spatial view.

Note: The scroll behavior seemed fine, that is, it always show the most recent selected gene (irrespective of the first/last aggregate strategy).

https://github.com/user-attachments/assets/9ca7c5d8-c1e2-4a19-8f08-aaf1c41d33e2






 and #2501
<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3a2b29ba5bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.