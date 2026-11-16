# Issue

**Title:** BCR tutorial

## Description

Added beta-version v2 of bcr tutorial and adapted corresponding file so that I (hopefully) can visualize it with read-the-docs. I have drastically reduced the tutorial as I was very unsatisfied with the previous version. I will add soon further literature to the .bib file and adapt the glossary to make the tutorial more precise and less overwhelming, while still providing any interested user with additional information.

I would be happy for any feedback (@FFinotello @grst) to make the tutorial as good as it could possibly be!

 

-   [x] Fix TODO comments
-   [x] CHANGELOG.md updated
-   [x] Tutorial updated (if necessary)
-   [x] rerun tutorial with latest version of scirpy once all required functionality is merged
-   [x] add CI test for tutorial
-   [x] review glossary

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5ffada9a48c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.