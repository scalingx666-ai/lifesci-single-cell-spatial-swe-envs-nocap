# Issue

**Title:** Update template to v0.4.0

## Description

`cookiecutter-scverse` released [v0.4.0](https://github.com/scverse/cookiecutter-scverse/releases/tag/v0.4.0).

## Changes

## What's Changed
* pre-commit updates
* Fix installation instructions on contributing guide by @grst in 
* fix typo by @Zethson in 
* Use cookiecutter variable for project repo in conf.py by @Zethson in 
* Add node_modules to .gitignore by @Zethson in 
* Update required python versions according to scientific python SPEC 0 by @grst in 
* Require myst-nb >= 1.1.0 by @grst in 


**Full Changelog**: https://github.com/scverse/cookiecutter-scverse/compare/v0.3.1...v0.4.0

## Additional remarks
* unsubscribe: If you don’t want to receive these PRs in the future,
  add `skip: true` to [`template-repos.yml`][] using a PR or,
  if you never want to sync from the template again, delete your `.cruft` file.
* If there are **merge conflicts**,
  they either show up inline (`>>>>>>>`) or a `.rej` file will have been created for the respective files.
  You need to address these conflicts manually. Make sure to enable pre-commit.ci (see below) to detect such files.
* The scverse template works best when the [pre-commit.ci][], [readthedocs][] and [codecov][] services are enabled.
  Make sure to activate those apps if you haven't already.

[`template-repos.yml`]: https://github.com/scverse/ecosystem-packages/blob/main/template-repos.yml
[pre-commit.ci]: https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#pre-commit-ci
[readthedocs]: https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#documentation-on-readthedocs
[codecov]: https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#coverage-tests-with-codecov

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `749fd270280d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.