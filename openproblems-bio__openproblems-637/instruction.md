# Issue

**Title:** add SCALEX to batch_integration

## Description

<!-- You can erase any parts of this template not applicable to your Pull Request. -->

[SCALEX](https://www.nature.com/articles/s41467-022-33758-z) claims to outperform the SoTA currently in our benchmark. I figured adding it would be the easiest way to find out for myself :)

### Submission type

* [X] This submission adds a new method

### Testing

* [X] This submission was written on a forked copy of SingleCellOpenProblems
* [X] GitHub Actions "Run Benchmark" tests are passing on this base branch of this pull
  request (include link to passed test: https://github.com/scottgigante-immunai/openproblems/actions/runs/3283518714/jobs/5409826099)

### Submission guidelines

* [X] This submission follows the guidelines in our
  [Contributing](../blob/master/CONTRIBUTING.md) document
* [X] I have checked to ensure there aren't other open [Pull Requests](../pulls) for the
  same update/change

### PR review checklist

This PR will be evaluated on the basis of the following checks:

* [X] The task addresses a valid open problem in single-cell analysis
* [X] The latest version of master is merged and tested
* [X] The methods/metrics are imported to `__init__.py` and were tested in the pipeline
* [X] Method and metric decorators are annotated with paper title, year, author, code
  version, and date

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b460ecb18332`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.