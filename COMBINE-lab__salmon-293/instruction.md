# Issue

**Title:** Add cmakelint script to check cmake format.

## Description

This PR is related to  .

It is to add lintcheck for cmake files.

## How to use

```
$ pip3 install cmakelint

$ which cmakelint
/path/to/cmakelint

$ ./scripts/lint.sh
```

Every CMakeLists.txt or *.cmake file in this repository is target for the check.
Right now I only modified `./CMakeLists.txt` to show for the example, and changed the permission of the executable bit file. Maybe the executable bit is not necessary.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `093b5a98e16c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.