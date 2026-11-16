# Issue

**Title:** Allow to set k_neighors in perplexity based affinity

## Description

This should implement my suggestion in #156.

I checked and it seems to work as expected. 

However, notice that I changed the logic in `to_new` and in `set_perplexity` a little, to make it consistent with `k_neighbors` that could possibly be user-provided. For simplicity, I made these functions always use the same originally provided or computed `k_neighbors` neighbors. So e.g. if the original affinity is computed with `perplexity=20, k_neighbors=25`, then `to_new(perplexity=10)` will use the same `k_neighbors=25`. Previously your code would have used 3*10=30 in this case (which won't work in this particular situation because 25<30).

The same for `set_perplexity`. 

This may result in some loss of efficiency, but I thought it's probably negligible. Let me know what you think.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d69c12d65f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.