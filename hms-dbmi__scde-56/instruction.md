# Issue

**Title:** Pin flexmix to 2.3-13.

## Description

This PR pins flexmix to version 2.3-13. This way if a user installs scde via GitHub, they won't experience the known errors caused by changes introduced in flexmix 2.3.-14.



xref: #40 #48 and [Google Group discussion](https://hms-dbmi.github.io/scde/help.html?place=msg%2Fsinglecellstats%2FrbFUTOQ9wu4%2Fyg4cxLbeAAAJ)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5d2744240db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.