# Issue

**Title:** Fix codecov CI and update template

## Description

This PR fixes some problems with the CI setup of the scverse-cookiecutter template repo. Last night, [the `codecov` package was pulled from PyPI](https://community.codecov.com/t/codecov-yanked-from-pypi-all-versions/4259). This can easily be replaced, however we've realized our automatic template sync system does not allow us to modify github actions (a security precaution from github), so we need to roll out this update manually.

We're also taking this opportunity to make several other intended changes for to the CI workflow.

We're still looking into how we can avoid this in the future, which will likely require us changing how our template sync system works. This is being tracked in the .

## Changes

These changes constitute the 0.2.1 release of the template and make the following changes:

* Remove codecov as a dependency since it's been pulled from pypi (scverse/cookiecutter-scverse#161)
* Remove usage of deprecated GitHub actions environment variables (these will be removed in a month) (scverse/cookiecutter-scverse#161)
* Fix some spurious ruff errors ( scverse/cookiecutter-scverse#156, scverse/cookiecutter-scverse#159 )
* Replace the example citation with the scverse manuscript ( scverse/cookiecutter-scverse#160 )
* automatically cancel running CI jobs on new commit (scverse/cookiecutter-scverse#158)

## Additional remarks
* If there are **merge conflicts** a `.rej` file will have been created for the respective files. You need to address these conflicts manually. Make sure to enable pre-commit.ci (see below) to detect such files.
* The scverse template works best when the [pre-commit.ci](https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#pre-commit-ci), [readthedocs](https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#documentation-on-readthedocs) and [codecov](https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#coverage-tests-with-codecov) services are enabled. Make sure to activate those apps if you haven't already.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ac5e65fa54b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.