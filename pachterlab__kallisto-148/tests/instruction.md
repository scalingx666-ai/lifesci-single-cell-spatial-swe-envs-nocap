# Issue

**Title:** Fix CMake

## Description

* Respect user variables. Set default `CMAKE_BUILD_TYPE`, and
  do not override user `CXXFLAGS`.
* Use `GNUInstallDirs` to allow changing directory where
  kallisto gets installed to.
* Use modern CMake idioms to detect C++11, which is more
  generalizable than adding `-std=c++11` unconditionally.
* Fix some minor C++ issues for building unit tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0383fae96298`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.