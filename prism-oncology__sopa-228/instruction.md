# Issue

**Title:** Corrected channel order for channel name input from TIF metadata in CosMx reader

## Description

Adjusted indexing of the CosMx reader's TIF metadata scraper to ensure channels are output in the same order as they were when `Morphology_ChannelID_Dictionary.txt` was used to get channel names. #180

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bd238aa56c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.