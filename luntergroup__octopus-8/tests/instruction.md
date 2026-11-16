# Issue

**Title:** htslib build fixes

## Description

These are some minor modifications to htslib detection so that octopus can be build from an htslib installation in a non-standard location (as conveyed by specifying `HTSLIB_ROOT` during configuration). In theory the code does this already, but it currently detects the wrong include directory -- the htslib include directory should not contain the final "htslib" directory -- instead all client code should add this directory in the #include, eg. `#include "htslib/foo.h`.

Besides adjusting the detected include, I removed the redundant `HTSLIB_ROOT` hint (this is already added to `HTSLIB_SEARCH_DIRS`), removed an include which relies on the incorrect include path, and reordered the hts library names so that the static library will be preferred, so that less dynamic search path wrangling is required when a custom htlib install location is used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3277f2fe2294`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.