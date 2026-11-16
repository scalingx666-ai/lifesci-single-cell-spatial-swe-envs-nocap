# Issue

**Title:** Bump node version in release workflow

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
To fix

```
Run npm install -g npm@latest
npm error code EBADENGINE
npm error engine Unsupported engine
npm error engine Not compatible with your version of node/npm: npm@12.0.1
npm error notsup Not compatible with your version of node/npm: npm@12.0.1
npm error notsup Required: {"node":"^22.22.2 || ^24.15.0 || >=26.0.0"}
npm error notsup Actual:   {"npm":"10.8.2","node":"v20.17.0"}
npm error A complete log of this run can be found in: /home/runner/.npm/_logs/2026-07-14T20_10_50_987Z-debug-0.log
Error: Process completed with exit code 1.
```

<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `051ffe5eeb7c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.