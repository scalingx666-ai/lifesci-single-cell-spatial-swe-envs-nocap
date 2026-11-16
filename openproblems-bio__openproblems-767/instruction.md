# Issue

**Title:** Add pymde to dimensionality reduction

## Description

<!-- You can erase any parts of this template not applicable to your Pull Request. -->

### Submission type

* [X] This submission adds a new method

### Testing

* [X] This submission was written on a forked copy of openproblems
* [X] Nextflow test pipeline is passing on this base branch of this pull
  request (include link to passed test on NF Tower found in GitHub Actions summary: https://tower.nf/orgs/openproblems-bio/workspaces/openproblems-bio/watch/4joeXe0YpqR4dQ)

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
* [X] The README gives an outline of the methods, metrics and datasets in the folder

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14d70b330cae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.