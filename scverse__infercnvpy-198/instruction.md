# Issue

**Title:** chore: point URLs to scverse, drop changelog stub

## Description

Summary: The repository moved from icbi-lab to scverse, so this PR updates the links that still point to the old location and moves the release notes to GitHub releases.

Changes:
- `pyproject.toml` project URLs now point to `scverse/infercnvpy`. I also added `Changelog`, `Issues` and `Forum` entries, following mantispy.
- The README badges, install command and issue tracker link use the new location. The tests badge linked to `test.yml`, but the workflow file is `test.yaml`, so the link is fixed too.
- `docs/conf.py` and `.cruft.json` use `github_user = "scverse"`, so the docs "edit on GitHub" links and future template updates use the right repository.
- The example dataset `base_url` points to the scverse release asset. The old URL still worked through GitHub's redirect, but the redirect would break if anyone recreated `icbi-lab/infercnvpy`.
- `CHANGELOG.md` was only a pointer to the GitHub release page, so it is deleted together with `docs/changelog.md`. The README and `urls.Changelog` link to the releases page, and `CHANGELOG.md` is added to the cruft skip list so a template update doesn't bring it back.

Testing: The pre-commit hooks pass on the changed files, and the new dataset URL returns 200. I didn't build the docs locally, so the docs CI job is the check for the removed changelog page.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b32493589a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.