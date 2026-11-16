# Issue

**Title:** Added a travis testing config

## Description

New config file that tells Travis how to run. Just a few basic commands using the test data in the repo so far, can be extended to run with different command line options etc to try to cover all running modes.

To make this run, you'll need to activate Travis for the repo. Go to https://travis-ci.org and log in, then hit the little tick box to enable testing for this account.

Once that's enabled, a test will run for every commit and PR. If you enable it before you merge this, it should run once it's merged I think.

Phil

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `766274c5fb87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.