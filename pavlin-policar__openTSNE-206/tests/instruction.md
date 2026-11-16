# Issue

**Title:** Change default affinity model to multiscale

## Description

##### Issue
It is annoying to have to use Multiscale affinities, because we have to instantiate a separate `Multiscale` class.

##### Description of changes
By default, we used `PerplexityBasedNN`, which -- under the hood -- just converted the perplexity to single-element list and called the same underlying machinery that `MultiscaleMixture` did. In this PR, I change the default perplexity model to `MultiscaleMixture`, which allows calls like
```python
tsne = TSNE(perplexity=[50, 500])
# or
embedding.transform(x_new, perplexity=[10, 50])
```

This doesn't have any breaking changes and will produce the same results as before, but will be more flexible.

The parameter naming is a bit annoying/confusing. Currently, I've made it so that both the `TSNE()` constructor and `transform` both only accept `perplexity` and not `perplexities`.

##### Extra
- Also adds support for Python 3.10 ()
- Fixes potential bug on MacOS builds using clang-13, where we need to add -fno-finite-math-only flag

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd0924b10f3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.