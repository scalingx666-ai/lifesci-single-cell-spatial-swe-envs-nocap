# Issue

**Title:** Add Needleman-Wunsch distance as a faster alignment metric

## Description

## Summary

This PR adds a Numba-optimized Needleman-Wunsch sequence distance metric via `metric="needleman_wunsch"`. Conceptually, this metric is very similar to the existing alignment metric, with two main differences: it is much faster for large datasets, and it uses a linear gap model, where every gap position receives the same penalty.

The existing alignment metric allows gap openings and gap extensions to be penalized differently. However, this distinction is not used with the current default parameters anyway, where `gap_open == gap_extend`. If the alignment metric is configured such that `gap_open == gap_extend == gap_penalty`, both metrics should return equal results.

The reason for using a linear gap model is mostly practical. Supporting separate gap-open and gap-extension penalties requires handling three dynamic programming matrices instead of one for each sequence pair, which adds substantial computational overhead. For CDR3 sequences, which are usually quite short, I would generally expect users to choose parameters that allow only a limited number of gap positions. For example, in my test runs I used `cutoff=10` and `gap_penalty=4`, which allows up to two gap positions. In this setting, distinguishing between two separate single-position gaps and one adjacent two-position gap is probably not worth the additional runtime. Therefore, I do not think the restriction to a single gap penalty is a major limitation.

The problem with the current alignment metric is that it is too slow for large datasets. The `fastalignment` metric improves runtime, but it can also suffer from performance limitations and does not always return exact results. Besides that, the current default parameters do not allow gaps (`cutoff=10`, `gap_open=gap_extend=11`). In that default setting, only equal-length sequences can fall below the cutoff, so the metric effectively computes alignment distances between equal-length sequences without making use of meaningful gap placement.

Therefore, I implemented the Needleman-Wunsch distance in a similar style to the Numba-optimized TCRdist CPU implementation. It supports BLOSUM62 by default and can also use TCRBLOSUM alpha/beta matrices through `base_matrix="tcrblosum"`. With the improved performance, I was able to run the 8 million-cell Omniscope COVID dataset with 64 CPU cores using `cutoff=10` and `gap_penalty=4` within around 12 hours.

Overall, I think this metric is a useful addition because it provides an exact alignment-based distance that can still handle larger datasets. It is more flexible than the Hamming distance, but substantially faster than the existing alignment metric. In contrast to TCRdist, it is also not specific to TCR CDR3 sequences and can therefore be used for BCR analyses as well.

The most useful default values for `gap_penalty` and `cutoff` are open for discussion, since the performance improvements make less restrictive parameter choices feasible. It could also be discussed whether the existing alignment metric is still needed if its additional gap parameterization and support for additional Parasail substitution matrices are not required.

## Main changes

- Add `NeedlemanWunschDistanceCalculator` and expose it via `metric="needleman_wunsch"` in `sequence_dist` and `ir_dist`.
- Support BLOSUM62 and TCRBLOSUM alpha/beta substitution matrices in a similar way as the TCRdist metric.
- Implement a Numba-based Needleman-Wunsch dynamic programming algorithm with cutoff-based optimizations.
- Add test cases.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79a83440e71a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.