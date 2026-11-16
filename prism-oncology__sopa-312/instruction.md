# Issue

**Title:** Fix CosMx morphology marker names that have forward slashes in them

## Description

. Forward slash is the only potentially invalid character in CosMx morphology marker names. This fix changes the key from the Morphology2D TIFFs to be identical to the format used in the flatfiles (i.e. a period instead of a forward slash).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51252b32d937`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.