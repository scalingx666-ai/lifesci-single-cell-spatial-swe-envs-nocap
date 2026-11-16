# Issue

**Title:** build: find the OpenMP runtime macOS installs outside the search path

## Description

On macOS, `setup.py`'s OpenMP probe fails even when `libomp` is installed, and the build quietly falls back to a single-threaded extension with only a warning. Apple's clang ships no OpenMP runtime, and every common way of installing `libomp` (Homebrew on Apple Silicon or Intel, MacPorts) puts it where the compiler does not look. So every threaded code path (`n_jobs`) on a Mac currently runs on one core.

This is the first of a series of PRs that split up the performance work on `claude/opentsne-cython-perf-69a550` into reviewable pieces. It goes first because it is independent of the others and is the change a Mac user notices most.

## Changes (`setup.py` only)
- **Find `libomp` outside the default search path.** The probe searches the known Homebrew and MacPorts prefixes and asks `brew --prefix libomp`. When it finds the runtime, it adds the include and library directories and an rpath.
- **The probe links against the runtime.** A header without a matching library now counts as "not found", instead of giving a build that fails at import.
- **Architecture tuning on arm64/aarch64.** These machines previously got no tuning flags. They now get `-mcpu=native -mtune=native`, like x86 gets `-march=native`. As before, tuning is skipped when `AZURE_BUILD` or `CONDA_BUILD` is set, so distributed wheels are unaffected.
- **Every tuning flag goes through a `-Werror` probe.** Compilers accept an unknown `-m` flag with only a warning, so a plain compile never showed whether the flag was applied.

## Measurements
M1 Pro, a plain `python setup.py build_ext --inplace` with no OpenMP environment variables:

| | before | after |
|---|---|---|
| OpenMP in the build | no (falls back to serial) | yes, `libomp` linked |
| Barnes-Hut negative gradient, 44 808 points, 1 thread | 51.4 ms | 51.4 ms |
| same, 8 threads | not possible (serial build) | 7.5 ms (**6.8×**) |

Re-checked on this branch, rebased onto current master: both `_tsne` and `quad_tree` link `libomp`, and the Barnes-Hut gradient on 40 000 random points takes 235 ms on 1 thread and 39 ms on 8.

## Tests
`pytest tests`: 167 passed, 48 skipped, 1 failed. The failure is `test_affinities.py::TestGenericAffinity::test_call_with_custom_metric_with_unsupported_knn`. It requires `hnswlib`, which was not installed in that environment, and it is unrelated to this change.

## Notes for review
- On a local build, the linker warns that Homebrew's `libomp` was built for a newer macOS than the default `-mmacosx-version-min`. This is inherent to linking a Homebrew library and affects local builds only.
- The commit does a little more than OpenMP detection: it also adds the arm64 tuning and probes each tuning flag. These can go in a separate PR if you prefer.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b0f8a883ef4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.