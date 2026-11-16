# Issue

**Title:** Move loading data to separate thread to prevent freezing viewer

## Description

As long time freezing viewer is something not nice for user. Even with speedup loading of data, it could take multiple seconds for big data. 

This PR moves loading data and creating `Layer` to a separate thread, keeping the viewer responsible during load time. 
It indicates loading using a progress bar above the selection widget.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `802b8129c9f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.