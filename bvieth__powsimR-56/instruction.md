# Issue

**Title:** change package for computeSpikeFactors from scran to scuttle

## Description

Hi,
during installation, I got an error for the computeSpikeFactors as it seems that it is not within the scran package anymore. It is not in the scuttle package.
I changed the namespace and the installation worked.
Hope this helps.
Cheers,
Gianni

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49fd9516e240`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.