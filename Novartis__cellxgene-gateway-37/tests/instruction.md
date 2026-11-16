# Issue

**Title:** Migrated PR checks to GitHub actions

## Description

Tagging @alokito.

Partly a protest against Travis CI for instituting build time limits for even open source projects, and partly because GitHub Actions do have a few advantages:

1. A tad more organization
2. Parallel builds, unlimited build time.

I've gotten a bit of practice on  and [Network Analysis Made Simple](https://github.com/ericmjl/Network-Analysis-Made-Simple/actions/runs/445659815), and I think you'll enjoy it too.

Apologies about PR-ing from `master`, my fingers moved a tad too fast for myself. I'll be deleting my fork if this PR is merged or closed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21ff56ea8b15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.