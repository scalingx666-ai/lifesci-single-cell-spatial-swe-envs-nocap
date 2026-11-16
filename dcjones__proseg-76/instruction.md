# Issue

**Title:** init docker publish workflow

## Description

I noticed the cirro workflow relies on a docker image that doesn't seem to be public, nor linked directly to Proseg releases. This workflow will release a minimal container hosted based on the image defined and managed by the proseg repo (you) and updated with each official tagged release you make on github. It was a little weird to test as forks don't really work well with publish workflows, but it worked ok with a new repo I made with all the same contents. Feel free to reject this if you don't want it, but I know at least I would use it to run proseg standalone, and it might help the cirro workflow stay current with proseg updates.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `feefb23ddb7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.