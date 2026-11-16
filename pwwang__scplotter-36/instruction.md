# Issue

**Title:** ci: avoid Conda dependency when building spatial vignette

## Description

The release build fails while rebuilding the spatial vignette because `loadGiottoMini()` attempts to discover Conda, which is not available on the runner.

- **Change**
  Disable Giotto’s optional Conda setup only for the R-only dataset load, then restore the previous option.

  ```r
  g <- local({
    old_option <- options(giotto.use_conda = FALSE)
    on.exit(options(old_option))
    suppressWarnings(GiottoData::loadGiottoMini("vizgen"))
  })
  ```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab51d7626606`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.