# Issue

**Title:** Tkakar/fix 2688

## Description

The debugging of on-demand mesh loading not working on prod but working on dev revealed the underlying issue of how Docusaurus was compiling [...set]. Fixed in the `babel.config.js` instead of changing individual instances in the code

Also updates the devonvoluted H&E in the kiemen config

<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable
 - [ ] New subpackage(s) manually published to NPM and trusted publishing enabled, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be22edd09dc0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.