# Issue

**Title:** Improve BPCells compatibility (JackStraw + RunPCA)

## Description

These are some changes brought about from , then referenced in Seurat issue #8267

1. Make the `JackStraw` function compatible with BPCells objects. This approach shuffles the matrix subset as a dense matrix, but leaves the remainder of the data on-disk. For best performance the BPCells object should be stored in row-major order so that the matrix subsets can be performed efficiently, but it will work either way.
2. Improve performance of `RunPCA` by using the BPCells svds function. This takes advantage of the same solver RSpectra uses, but at the C++ level to avoid overheads of repeatedly creating BPCells C++ objects on each solver iteration. It also avoids the pitfall that irlba can only use its fast C version with in-memory matrices and otherwise falls back to a slower pure-R implemenation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `727c71a45e30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.