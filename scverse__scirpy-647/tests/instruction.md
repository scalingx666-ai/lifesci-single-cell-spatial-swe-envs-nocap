# Issue

**Title:** Update template to v0.6.0

## Description

`cookiecutter-scverse` released [v0.6.0](https://github.com/scverse/cookiecutter-scverse/releases/tag/v0.6.0).

## Changes

## CI updates

We now more consistently embrace hatch and uv in the template. CI now generates the job matrix from that hatch configuration. This means the `pyproject.toml` file is now the one **single** point of truth for both local and CI test jobs. 

* Get test matrix from hatch by @grst in 
* Enable parallel testing with hatch by @grst in 
* chore: update code cov by `@ilan-gold` in 
* Fix remaining uv cache globs in workflows by `@flying-sheep` in 
* Switch root tests to uv by `@flying-sheep` in 
* Fix uv cache glob for script tests by `@flying-sheep` in 
* Test pre-release dependencies by @grst in 
* Use hatch on RTD by @grst in 
* Fix ruff-check naming by `@Zethson` in 
* fix codecov upload () by `@ilia-kats` in 


## Documentation updates

We improved the "contributing guide" that is also synced into the repos using this template to recommend hatch
as the default project manager.

* Fix repo migration commands by `@le-ander` in 
* Delete docs/Makefile by @grst in 
* restore missing links by `@Zethson` in 
* Update documentation by @grst in 


## Chore

* Update pre-commit config
* Re-enable dry-run for release by @grst in 
* Create template sync PRs from versioned branch by @grst in 


**Full Changelog**: https://github.com/scverse/cookiecutter-scverse/compare/v0.5.0...v0.6.0

## Additional remarks
* **unsubscribe**: If you don’t want to receive these PRs in the future,
  add `skip: true` to [`template-repos.yml`][] using a PR or,
  if you never want to sync from the template again, delete the `.cruft.json` file in the root of your repository.
* If there are **merge conflicts**, you need to resolve them manually.
* The scverse template works best when the [pre-commit.ci][], [readthedocs][] and [codecov][] services are enabled.
  Make sure to activate those apps if you haven't already.

[`template-repos.yml`]: https://github.com/scverse/ecosystem-packages/blob/main/template-repos.yml
[pre-commit.ci]: https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#pre-commit-ci
[readthedocs]: https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#documentation-on-readthedocs
[codecov]: https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#coverage-tests-with-codecov

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b16c2ccc64a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.