# Issue

**Title:** update for compatibility with the new version of GSVA

## Description

Dear scGSVA team,

Thanks for this great package!

Du to a major update in the package `GSVA`, the `gsva` function is defunct. From the GSVA doc:

```
Instead of gsva(expr=., gset.idx.list=., method=., ...), use a method-specific parameter object, see plageParam, zscoreParam, ssgseaParam, gsvaParam, gsvaParam, followed by a call to the new gsva() function, see gsva
```

I tried to fix this in this PR but you might want to further test it.

Best,
-E

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca3b228c6e6b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.