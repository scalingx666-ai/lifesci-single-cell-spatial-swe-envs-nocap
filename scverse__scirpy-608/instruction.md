# Issue

**Title:** Update template to v0.5.0

## Description

`cookiecutter-scverse` released [v0.5.0](https://github.com/scverse/cookiecutter-scverse/releases/tag/v0.5.0).

## Changes

### New template sync

We re-implemented template sync from scratch instead on relying on cruft. This allows us to create *real merge conflicts* that show up as such on GitHub instead of `.rej` files. 

* Generate real merge conflicts on template update by @grst in 

### Enhancements

We committed to using [hatch](https://hatch.pypa.io/latest/) as project and environment manager. By doing so, we simplified the 
GitHub actions: 
* Hatch envs by @flying-sheep in 
* Upgrade Github actions by @Zethson in  
* Use hatch in github actions by @grst in 

We switched the pre-commit hook from prettier to biome and added a pre-commit hook for autoformatting `pyproject.toml` files:
* Switch from prettier to Biome by @flying-sheep in 
* TOML formatting using pyproject-fmt by @flying-sheep in 

We added (optional) integration with VScode and improved cookiecutter prompts:
* Add VS Code integration by @flying-sheep in 
* Add prompts for most variables by @flying-sheep in 

We removed bump2version as recommended way to update versions. Instead, just update the version manually in `pyproject.toml` or use [hatch-vcs](https://cookiecutter-scverse-instance.readthedocs.io/en/latest/template_usage.html#using-vcs-based-versioning)
* Remove bump2version by @Zethson in 


### Fixes
* Fix PyPI link in README by @grst in 
* Fix autosummary template by @flying-sheep in 
* Fix string syntax in hook output by @flying-sheep in 
* Fix repo metadata by @flying-sheep in 
* Fix links by @flying-sheep in 
* Update post-gen output for hatch by @flying-sheep in 
* Fix README links by @flying-sheep in 
* Hatch `extra-features` doesn’t exist by @flying-sheep in 
* Update / fix README template by @le-ander in 
* Exclude .cruft.json from biome hook by @grst in 
* Switch to session-info2 by @Zethson in 
* Use cruft in github action that creates instance repo by @grst in 
* Even more precautionary bash settings by @grst in 

### Documentation
* Add instructions on how to migrate an existing project to using the template by @grst in 
* fix hatch snippets for docs build in contributing.md by @eroell in 
* Add instructions for a pending publisher by @flying-sheep in 
* Add Github Actions documentation and simplify template usage by @Zethson in 
* Add more elaborate example by @Zethson in 
* Suggest to use `uv` to run cruft by @grst in 

### Chore

* Remove test reliance on unmaintained pytest-git by @flying-sheep in 
* pre-commit updates


## New Contributors
* @eroell made their first contribution in 
* @le-ander made their first contribution in 
* @scverse-bot made their first contribution in 

**Full Changelog**: https://github.com/scverse/cookiecutter-scverse/compare/v0.4.0...v0.5.0

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6abf5bae876e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.