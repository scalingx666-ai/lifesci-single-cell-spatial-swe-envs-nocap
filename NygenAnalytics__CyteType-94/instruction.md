# Issue

**Title:** Apply shared documentation styling

## Description

Add the tool logo to the README and use shared Nygen logos, favicons, styles and navigation assets throughout the documentation. Pin the MyST version and book theme, label the landing page Overview, and add a link to the documentation hub.

Reviewed existing generated output and verified the deployed shared assets. Fresh documentation builds should pass before merging.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ce97c558d43`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.