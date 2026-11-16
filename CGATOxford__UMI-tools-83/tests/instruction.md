# Issue

**Title:** {ts} update doc

## Description

Documentation update.

 #77 

Also uses six.iteritems() in place of dict.iteritems for py2/py3 compatibility. Note this wasn't picked up since quality thresholding with _extract_ was not previously covered by tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ff1703237b3d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.