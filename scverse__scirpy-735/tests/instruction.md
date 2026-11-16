# Issue

**Title:** Use scverse-misc for deprecations

## Description

Replace the home-grown `scirpy.util.deprecated` decorator and the ad-hoc
`warnings.warn` calls with the `deprecated` and `deprecated_arg` decorators
from `scverse-misc`, which also add a deprecation notice to the API docs.

`scverse-misc` is added as a hard dependency (no extras required; the
`[sphinx]` extra remains in the `doc` dependency group).

Deprecated functions:
  * `ir_dist.tcr_dist` (0.5.0)
  * `ir_dist.metrics.AlignmentDistanceCalculator` (0.15.0). The decorator moves
    from `__init__` to the class so the notice appears in the class docs.

Deprecated arguments:
  * `clip_at` of `tl.clonal_expansion` and `pl.clonal_expansion` (0.14.0)
  * `block_size` of the `ParallelDistanceCalculator`s (0.15.0)
  * `include_fields` (0.13.0) and `use_umi_count_col` (0.16.0) of the
    `io.read_*` functions
  * `cached`/`cache_path` of `datasets.vdjdb` and `datasets.iedb` (0.24.0)

The latter two groups previously did not emit any warning at all and now
consistently raise a `FutureWarning`.

Since `deprecated_arg` warns whenever the deprecated argument is passed
(irrespective of its value), internal calls must not forward it:
`pl.clonal_expansion` now converts `clip_at` into `breakpoints` itself instead
of passing it on to `tl.clonal_expansion`, and the alignment distance
calculators no longer forward the ignored `block_size` to their base class.





- [x] CHANGELOG.md updated
- [x] Tests added (For bug fixes or new features)
- [ ] Tutorial updated (if necessary)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02ad919263d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.