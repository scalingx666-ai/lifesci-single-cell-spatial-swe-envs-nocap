# Issue

**Title:** Re-implementating co_occurrence()

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description

Togeter with [@MDLDan](https://github.com/MDLDan) we reimplement the `squidpy.gr.co_occurrence()` function using Numba. 
The new algorithm removes the need for a pre-calculated pairwise distance matrix, enabling it to handle large datasets without splitting. Parallel processing is enabled by default, increasing the runtime speed by 40 times.
![image](https://github.com/user-attachments/assets/83f6778f-70f8-4d83-aff2-a024a67fecc2)

We also implemented it in Rust using PyO3 and achieved similar performance. We chose to push the Numba implementation.

Following issues are related:





## How has this been tested?

- All `squidpy.gr.co_occurrence()` related have passed in `squidpy` package test. 
- We also compared the new and old implementations output:
   - Until the number of cells do not require squidpy to split the differences are in the 1e-08 range.
   - When the number of cells requires squidpy to spit differences are in the order of 1e-02 see (.

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `349b75afbd26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.