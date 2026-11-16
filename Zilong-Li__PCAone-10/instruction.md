# Issue

**Title:** Add support for ARM-based systems (e.g. aarch64 Linux)

## Description

The previous `Makefile` contained several hardcoded compiler flags and library paths that are specific to the `x86_64` architecture. This caused the build to fail on other platforms, such as ARM-based Linux systems.

This patch adds conditional logic into the `Makefile` to apply settings only on appropriate systems. I also added workflow_dispatch to allow for manual triggering of the GitHub Actions.

- The `Makefile` now uses `uname -m` to detect the system's CPU architecture at the start of the build process.
- Conditional `x86_64` Flags:** The `-m64`, `-mavx2`, and `-mfma` compiler flags are now wrapped in a conditional block and are only applied when the detected architecture is `x86_64`.

These changes ran successfully on GitHub actions: https://github.com/SauersML/PCAone/actions

Locally, on aarch64 Linux, the changed code was able to build and run successfully on real data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `477520cdd4e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.