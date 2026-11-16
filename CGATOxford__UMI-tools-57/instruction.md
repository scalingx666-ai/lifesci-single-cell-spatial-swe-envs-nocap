# Issue

**Title:** Group

## Description

@IanSudbery 

The group branch includes a new command "group" which will attempt to identify the group of UMIs which come from the same True UMI + errors and output either a tagged BAM and/or a flatfile detailing the UMI groups.

To achieve this, much of the code originally in umi_tools/dedup.py was refactored into two module files, network.py and umi_methods.py (this could do with a better name). In additional, the functionality of the twopasswriter method was expanded to allow addition of tags to reads and the functionality of the ClusterAndReducer functor (renamed ReadClusterer) was expanded to allow the use of the functor for grouping as well as deduplicating.

I'll leave the merging until you've had a chance to look over the code. There is no urgency to merge back into master immediately.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `978534c9e868`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.