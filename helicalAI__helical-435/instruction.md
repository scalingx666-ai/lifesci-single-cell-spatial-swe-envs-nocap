# Issue

**Title:** ci(soc2type2): push v* release tags with the helical-release-bot token

## Description

Part of the v* tag protection in helicalAI/github-configs#12. The `helical-release-tags` org ruleset will block `v*` tag pushes made with `GITHUB_TOKEN`, and GitHub does not accept the `github-actions` app as a ruleset bypass actor. The bypass actor is the `helical-release-bot` GitHub App instead.

In the `release` job, this PR mints a `helical-release-bot` token with `actions/create-github-app-token` (v3.2.0, pinned by SHA) and passes it to `actions/checkout`. Checkout stores it as the git credential, so the existing `git push origin "v…"` runs as the app.

**Merge order:** merge after the `RELEASE_BOT_PRIVATE_KEY` org secret and `RELEASE_BOT_CLIENT_ID` org variable exist (step 1 of the apply order in helicalAI/github-configs#12), and before the ruleset is applied. Until the secret exists, the token step fails and the release job stops before tagging.

Refs:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `706c13f7b8c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.