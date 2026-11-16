# Issue

**Title:** Add in ability to set a temporary directory

## Description

Add in a new option to many of the subcommands to set the directory for temporary files. I didn't know which subcommands actually used temporary files so I added the option to all of them minus the plot generating ones. I implemented it as a custom action for the option parser so that I didn't need to modify too much of the code. These changes fixed issue #9

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7831f1359a4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.