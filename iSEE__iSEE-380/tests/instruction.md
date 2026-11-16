# Issue

**Title:** Prepared interface elements, class slots for global selection.

## Description

Deals with #377. Note that it is best that the global on/off does not interfere with the selection source, only modifying the underlying graph by adding or removing the link and retriggering the necessary plotting events.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c391b8dfadef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.