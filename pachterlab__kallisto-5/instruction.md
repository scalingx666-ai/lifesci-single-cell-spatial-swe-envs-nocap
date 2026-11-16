# Issue

**Title:** Get test suite working & fix CMakeLists.txt

## Description

- Compile time improved by removing extra includes of Catch
- Remove Catch as a submodule
- Include scripts to add Catch as a CMake external project
- Remove fasta tools
- Remove test_sequences
- Start testing index writing and loading

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b3ba93a3228`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.