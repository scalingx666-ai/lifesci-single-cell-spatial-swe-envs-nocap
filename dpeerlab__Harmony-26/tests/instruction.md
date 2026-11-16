# Issue

**Title:** replace fa2 dependency

## Description

It became increasingly hard to install the `fa2` dependency. This PR replaces it with the better maintained [fa2-modified](https://github.com/AminAlam/fa2_modified) fork with an equivalent API.

I also bumped the version from `0.1.5` to `0.1.6`.

@ManuSetty

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `785d4ab9f016`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.