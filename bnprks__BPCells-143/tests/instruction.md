# Issue

**Title:** [r] Change default insertion mode for macs peak calling, rename function

## Description

Deprecating `call_macs_peaks()` to `call_peaks_macs()` as discussed previously.  Note, is this how we should be handling deprecated APIs?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80bf57d0eb53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.