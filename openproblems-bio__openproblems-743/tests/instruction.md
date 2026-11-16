# Issue

**Title:** [Dimensionality reduction] Fix RMSE metric

## Description

<!-- You can erase any parts of this template not applicable to your Pull Request. -->

.

### Submission type

* [X] This submission adds a new metric
* [X] This submission fixes a bug (link to related issue: #742)

### Testing

* [X] This submission was written on a forked copy of openproblems
* [ ] Nextflow test pipeline is passing on this base branch of this pull
  request (include link to passed test on NF Tower found in GitHub Actions summary: )
* [X] If this pull request is not ready for review (including passing the Nextflow test
  pipeline), I will open this PR as a draft (click on the down arrow next to the
  "Create Pull Request" button)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `becb1f6fe35a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.