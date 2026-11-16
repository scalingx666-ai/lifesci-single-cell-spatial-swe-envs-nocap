# Issue

**Title:** outfile.fetch in paired output writer.

## Description

Paired writer was calling fetch on outfile rather than infile to find unmatched pairs cf issue #50.

Can't think what I was thinking when I wrote this. Clearly the first person to run a paired file that had paired reads in it (or mates on a different chromosome) was going to trigger this error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `899a9b68fdca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.