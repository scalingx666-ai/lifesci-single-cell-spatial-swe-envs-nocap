# Issue

**Title:** NickAkhmetov/Add truncation for long channel names in spatial view legend

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
 
<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->

This PR adjusts spatial channel displays to truncate after one line instead of wrapping, to more gracefully handle cases where visualizations' spatial channels have long names.

<img width="3763" height="2053" alt="image" src="https://github.com/user-attachments/assets/c84b9241-1438-4666-800a-c840efc154d0" />


#### Change List
- Sets the max width for channel names to 90%, keeping the full name visible on mouse-over, and making sure the legend remains visible.

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable
 - [x] New subpackage(s) manually published to NPM and trusted publishing enabled, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ecebd488ae9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.