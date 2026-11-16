# Issue

**Title:** doc: fix docs for dedup stats filenames

## Description

Hi,

I noticed that the documentation and files produced with `dedup --output-stats` were inconsistent. 

https://github.com/CGATOxford/UMI-tools/blob/14661b496090d72ac40df82c27a27c0bded8cd96/umi_tools/dedup.py#L450

https://github.com/CGATOxford/UMI-tools/blob/14661b496090d72ac40df82c27a27c0bded8cd96/umi_tools/dedup.py#L391

https://github.com/CGATOxford/UMI-tools/blob/14661b496090d72ac40df82c27a27c0bded8cd96/umi_tools/dedup.py#L414

I've updated the docs to reflect the names used in the code. Please let me know if you need anything else to merge!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14661b496090`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.