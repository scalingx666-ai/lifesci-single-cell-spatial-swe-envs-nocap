# Issue

**Title:** docs: add CHANGELOG.md and CONTRIBUTING.md

## Description

## Summary

- **CHANGELOG.md**: a new change log covering every published release from 0.9.0 to 1.3.0, most recent first. It merges the GitHub release notes with the notes previously kept in `checkm/VERSION`, and uses PyPI for 0.9.1, 0.9.2 and 1.1.4, which were released only there. Dates come from the GitHub release, or from PyPI where there's no GitHub release. Versions that weren't released separately are listed under the release that first included them: 1.0.14 in 1.0.15, 1.2.6 in 1.2.7, and 1.2.8 and 1.2.9 in 1.2.10.
- **`checkm/VERSION`** now holds only the version number, so the change log is kept in one place. Only the first line was ever read (`setup.py`, `bin/checkm`, `docs/src/conf.py`).
- **Documentation site**: the change log page includes `CHANGELOG.md` through `myst-parser`, which is added to `docs/requirements.txt` and `conf.py`. The docs workflow now also runs when `CHANGELOG.md` changes.
- **CONTRIBUTING.md** replaces `CONTRIBUTING`. It covers:
  - the maintenance scope: CheckM v1 is unmaintained, and only compatibility fixes are accepted
  - how to report bugs
  - development setup, including `CHECKM_DATA_PATH`
  - running the tests
  - guidelines for changes and pull requests
  - the release process
  - acknowledgements of contributors, taken from git history, the release notes and the docs
- **Packaging**: removes the outdated `CHANGES.txt`, and `MANIFEST.in` now includes `CHANGELOG.md` in the sdist.

## Testing

- `make html SPHINXOPTS="-W --keep-going"` builds without warnings. The change log page shows one section per release, and the existing `:ref:`changelog`` links still resolve.
- `python setup.py sdist` builds `checkm_genome-1.3.0.tar.gz` with `CHANGELOG.md` included.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a92be4acd56c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.