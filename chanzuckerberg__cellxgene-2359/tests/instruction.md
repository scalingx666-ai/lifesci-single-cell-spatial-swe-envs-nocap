# Issue

**Title:** remove unused packages from client

## Description

This PR removes a number of unused package dependencies from package.json.  Some of these are completely unused, some are used by sub-dependencies and should not be in the top-level package.json:
* react-easy-emoji
* react-popper
* connect-history-api-fallback
* style-loader
* sw-precache-webpack-plugin
* url-loader

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01d34580b981`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.