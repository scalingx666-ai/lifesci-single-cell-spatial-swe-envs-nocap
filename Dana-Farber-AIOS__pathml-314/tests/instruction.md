# Issue

**Title:** pin protobuf to 3.20.1

## Description

Tests started failing unexpectedly: https://github.com/Dana-Farber-AIOS/pathml/runs/6749244149?check_suite_focus=true

The problem seems to be an error raised by the protobuf package. Checking the logs shows that the version of protobuf in the failing test ([4.21.1](https://github.com/Dana-Farber-AIOS/pathml/runs/6749244149?check_suite_focus=true#step:7:247)) is different from the one in the last passing test ([3.20.1](https://github.com/Dana-Farber-AIOS/pathml/runs/6482168049?check_suite_focus=true#step:7:248)). Other people have reported similar issue (). This PR pins protobuf version to 3.20.1 to try to fix the test suite

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52b72d6432f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.