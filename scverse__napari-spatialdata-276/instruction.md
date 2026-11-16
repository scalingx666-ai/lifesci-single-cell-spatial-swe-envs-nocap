# Issue

**Title:** fix: fix adjusting contrast limits for rgb data

## Description

While working on reproducing of performance problem for points and shapes, I found that adjusting contrast limits do not work for data with 3 channels, that are represented as RGB data. 

This PR contains the following changes:

1) change `channel_changed` from local function to class method 
2) generalize `_channel_changed` to accept any dimensional data. 
3) fix `AnnData` initialization for rgb data

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f4f425a828c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.