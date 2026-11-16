# Issue

**Title:** Use installed cereal and stadenio libraries if available.

## Description

There's been some issues with compiling salmon on macOS for some time now (see also ). In the current version, I was running into two compile errors on macOS:

1) problems with staden & Clang
2) problems with linking to boost static libraries

I could fix (1) by installing staden separately and then using that install in salmon. I've included the respective Find***.cmake files.

(2) is an easy fix by modifying the `CMakeLists.txt`. Is there any particular preference for using static libraries? This is a rather small patch and could be done in a Homebrew formula, if you prefer static boost libraries.

Otherwise, this PR are just suggestions. If you have changes that better conform to you style, that's fine by me.

Thanks,
Gabriel

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `433b773eabd5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.