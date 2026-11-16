# Issue

**Title:** {ts} ignore read pair suffixes

## Description

Resolves issue with '/1' and '/2' suffixes on read pairs (#325, #391, #418, )

As noted in #391, I have inadvertently made two completely separate patches to solve this issue, neither of which has been merged with master. This PR is my favoured resolution. The `--ignore-read-pair-suffixes` switch makes `joinedFastqIterate` remove the suffixes entirely since these are not required for downstream tools. 

@IanSudbery - I would appreciate a quick check before I merge. 

I'm not sure why the tests fail. They pass fine for me with linux and p3.6.7 (as per travis). I'll resolve this before merging though. [EDIT - Looks to be an upstream dependency issue. Restarting a travis job that passed 4 months ago also gives the same fails: https://travis-ci.org/github/CGATOxford/UMI-tools/builds/655549297]

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60ad2786ec2a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.