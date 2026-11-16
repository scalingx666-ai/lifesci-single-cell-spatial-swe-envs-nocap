# Issue

**Title:** Fix to have Load10X_Spatial recognize use.names for segmented data

## Description

Currently, Load10X_Spatial will not pass the use.names argument when loading segmented data.   The result is that feature IDs are always gene symbols regardless if use.names is set or not.  This fix updates the Load10X_Spatial function so that use.names will be passed to Read10X_h5 when loading segmented data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d519dda56a57`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.