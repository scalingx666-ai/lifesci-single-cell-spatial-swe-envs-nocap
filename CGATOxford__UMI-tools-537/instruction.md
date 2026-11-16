# Issue

**Title:** Altered if clasuses around selection of commands in umi_tools.py

## Description

Fixes (or at least starts to fix) #536 

@TomSmithCGAT Bit confused as to what is going on in the umi_tools module. Specifically what the original purpose of the if clause at lines 51-52 was.

I've also made each tool print its usage message if no options are passed at all. Don't know if this was the right was to do this, or if I should have done something more central (although that would become a problem if there was a tool that could be run without options. Which currently there isn't).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c182d795b44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.