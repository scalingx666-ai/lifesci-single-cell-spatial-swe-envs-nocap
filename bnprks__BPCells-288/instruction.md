# Issue

**Title:** [cpp] add version detection for highway

## Description

# Background
We use a package named highway, which helps with added efficiency in automatically choosing the best CPU intrinsics for vectorization based on your architecture.

Previously, there was a previous bug during compilation, which did not allow BPCells to utilize Highway if it was already installed. This was fixed. However, I suspect that if you have an older version of highway, installation would fail, and would not fall back to our packaged version of highway.  We can see this in #285, where `BroadcastLane`, which is part of highway is not being detected.

# Fix
I made some general improvements to `configure` for highway,  in both the logging and the detection.
I added some version detection within `hwy-test.cpp`, which is version templated through `hwy-test.cpp.in`.  I also added a fallback to using `pkg-config` found libraries, if the first compilation try fails.  There is also some additional clarity on whether the compilation fails because of versioning, or from failing to compile for a different reason.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d2a036af912`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.