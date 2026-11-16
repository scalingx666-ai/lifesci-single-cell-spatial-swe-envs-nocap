# Issue

**Title:** kit: recognize C++ source files in run evidence

## Description

A run that saves C++ code as `attempts/<lens>/code/search.cc` or `search.cxx`, together with its program output, currently fails with `needs at least one program it ran and that program's saved output`. These extensions are missing from `CODE_EXT`, so the checker counts the source as an output artifact and finds no program. The same mismatch affects `.hh` and `.hxx`; all four are already recognized by the existing source-placeholder policy's `SOURCE_EXTS`.

Add the four extensions to the shared code-file classification. Add workspace-level regression tests for the source/header extensions, uppercase `.CC`/`.CXX`, missing saved output, and plain-text files that do not constitute program evidence. No compiler or additional dependency is needed to run the tests.

Validation:

- The original main suite passes all 84 tests. With only the new tests added, the six source/header/uppercase subcases fail on main with the missing-program diagnostic.
- With the fix, all 87 tests pass on Linux with Python 3.11 and 3.14. The missing-output and plain-text controls still fail the workspace check as required.
- A trial merge with #629 is clean. In an isolated copy of the combined tree, all 87 tests pass under both Python versions with Windows text-write newline conversion emulated, including child Python processes. Native Windows validation remains pending.
- `git diff --check` passes.

The root release `SHA256SUMS` is left for the maintainer to refresh against the final merged tree.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d14b0098c7dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.