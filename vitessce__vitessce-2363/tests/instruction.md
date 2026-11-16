# Issue

**Title:** NickAkhmetov/Increase automatic scatterplot point size for improved visibility

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

<!-- For other PRs without open issue -->
#### Background
It has been expressed that the default point size on the scatterplot is very small/difficult to work with. 

This PR increases the baseline size of the automatically calculated points without affecting the other calculations.
#### Change List
- Increases baseline point size from 0.05 percent of the diagonal axis to 1 percent of the diagonal axis.
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

#### Screenshots
Default `codeluppi-2018` scatterplots (in expanded view) on production:
<img width="469" height="1370" alt="image" src="https://github.com/user-attachments/assets/4c2421fa-819a-4c35-a935-0adea13e1ce4" />


Default `codeluppi-2018` scatterplots (in expanded view) with this change:
<img width="469" height="1398" alt="image" src="https://github.com/user-attachments/assets/f0b32301-26bc-4048-a960-83b1ec599484" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1e4ffddb5b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.