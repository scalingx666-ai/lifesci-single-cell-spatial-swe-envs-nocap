# Issue

**Title:** Fix windows segfault

## Description

##### Issue
For some reason, `test_fft_transform_with_point_subsets_using_perplexity_nn` crashes with "Windows fatal exception: access violation" (segfault) in `estimate_negative_gradient_fft_2d`.


##### Description of changes
The problem turned out to be in the `/fp:fast` flag we passed to the MSVC compiler. It worked for the msvc-2019 version, but apparently, they introduced some other optimizations in the msvc-2022 version. This caused segfaults. We already have this disabled on unix systems via the following compiler flags:
```
"-ffast-math",
"-fno-finite-math-only",
"-fno-associative-math",
```

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a93df4e3c3b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.