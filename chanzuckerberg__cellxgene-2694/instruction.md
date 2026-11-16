# Issue

**Title:** chore: Python 3.12 (SCE-16)

## Description

This PR adds support for python 3.12 to Annotate

## Changes
- Tested 3.12 with compatibility [matrix](https://github.com/chanzuckerberg/cellxgene/actions/runs/10800450332/job/29959738239?pr=2694)
- Added to push tests
- Updated flatbuffers to 2.0.7 for python 3.12 compatibility
- Updated node to 18
- Added timeout to address flakiness (thanks @rainandbare !)
- Updated docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb743efd9a52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.