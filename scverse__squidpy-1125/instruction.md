# Issue

**Title:** feat: remove ligrec parallelize

## Description

[benchmark code](https://gist.github.com/selmanozleyen/97e3abec793555ab1fa9ec1e88575aaa)

[main](https://gist.github.com/selmanozleyen/33c63461d0ad15f59ad123fabc06e283) results
[pr](https://gist.github.com/selmanozleyen/f48d8f8f86c7b8d7bdb9ae225e3eceb8) results

Results compared:
```
python benchmarks/bench_ligrec.py --compare benchmarks/results


scenario         n_jobs   main (s)     PR (s)  speedup   change
---------------------------------------------------------------
large                 1      2.548      3.865    0.66x  -51.7%
large                 4      1.561      1.259    1.24x +  19.3%
large                 8      1.706      1.122    1.52x +  34.2%
many_perms            1      1.620      2.247    0.72x  -38.7%
many_perms            4      0.924      0.637    1.45x +  31.1%
many_perms            8      0.966      0.647    1.49x +  33.1%
medium                1      0.261      0.425    0.61x  -62.8%
medium                4      0.581      0.183    3.18x +  68.5%
medium                8      0.687      0.173    3.97x +  74.8%
xlarge                1      8.139      9.259    0.88x  -13.8%
xlarge                4     10.498      3.077    3.41x +  70.7%
xlarge                8     10.188      2.768    3.68x +  72.8%
```

both faster and cleaner code. this removes parallelize.

update: the reason main is faster when n_jobs=1 is because main sets also  `numba_parallel=True` so it's because it's still numba parallel even though it's one process.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1163c0d6f5a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.