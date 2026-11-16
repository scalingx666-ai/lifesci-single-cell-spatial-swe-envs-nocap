# Issue

**Title:** manual workflow for single dataset run via github actions

## Description

A small new github action workflow that submits an individual job to Google Batch.  No polling til done, just fire and forget.  Logs can be inspected in google batch, and outputs will go to a dev google bucket.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18263f4fe744`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.