# Issue

**Title:** Fix louvain version constraint for macOS Clang compatibility

## Description

## Summary

Add minimum version constraint `louvain>=0.8.0` to fix installation failures on macOS with newer Clang compilers.

## Problem

SpaGCN fails to install on macOS with newer Clang compilers (e.g., AppleClang 16+) due to a compilation error in the `louvain` dependency:

```
error: a function declaration without a prototype is deprecated in all versions of C [-Werror,-Wstrict-prototypes]
  132 | unsigned short int gss_get_warning_flag();
```

Without a version constraint, pip may install `louvain==0.7.x`, which vendors an outdated igraph C source with function declarations that don't comply with modern C standards.

## Solution

The issue is already fixed in `louvain>=0.8.0`, which updated the igraph C core:
- v0.8.0: Updated igraph C core to 0.10.2
- v0.8.1: Updated igraph C core to 0.10.6
- v0.8.2: Added support for python-igraph >= 0.11, updated C core to 0.10.10

## Compatibility Testing

Tested with the following environment:
- louvain: 0.8.2
- igraph: 1.0.0
- scanpy: 1.11.5
- SpaGCN: 1.2.9

**Test Results:**
- SpaGCN spatial domain identification on 3 datasets (Human Lymph Node, Human Heart, Mouse Brain) with multiple cluster configurations - **all passed**
- scanpy.tl.louvain with multiple resolutions (0.3, 0.5, 0.8, 1.0, 1.5) - **all passed**
- louvain.find_partition API tests - **all passed**

## References

- louvain-igraph CHANGELOG: https://github.com/vtraag/louvain-igraph/blob/master/CHANGELOG
- PR for igraph 0.11 support:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3d4f108eb3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.