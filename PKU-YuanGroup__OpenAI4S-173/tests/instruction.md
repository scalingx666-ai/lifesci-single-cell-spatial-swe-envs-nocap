# Issue

**Title:** chore(contributors): refresh the wall for CyrusAuyeung and muzimu217

## Description

## Summary

Content-only refresh of the Community Contributors wall, produced by running `scripts/update_contributors.py` against the live contributors API. No code changes.

- The wall goes from 18 to 20 people: `CyrusAuyeung` (3 commits) and `muzimu217` (2 commits) were in the API but had never been rendered.
- The order follows the current commit counts, which is why existing rows move.
- `ChampionZhong.png` changes because that account now uses a different avatar on GitHub.
- The bilingual file tables under `.github/contributors/` were written by the script itself. This is the first refresh since #171, and updating those tables by hand is exactly the step that PR removed.

The maintained recognition list still carries `EQSTLab` and `difficulttopickaname`, whose commits the contributors graph cannot see. `ChampionZhong` is now returned by the API, so `include_recognized_contributors` drops that entry on its own; the constant can be trimmed separately.

## Area and Change Type

- Docs
- Documentation

## Verification

```text
GITHUB_TOKEN=$(gh auth token) uv run --no-project --with pillow python scripts/update_contributors.py
# 20 contributors; circular pngs: 20 refreshed, 20 linked locally

uv run --no-project python scripts/check_directory_readmes.py
# 166 maintained directories, 1561 direct files/assets, complete bilingual coverage
```

Both walls render 20 entries, every PNG is 256x256 RGBA with transparent corners and an opaque centre, and the avatar directory holds nothing but the 20 images and its two READMEs. The offline suite is untouched by this change; CI covers it.

## Risk and Reviewer Focus

The wall reorders on every refresh, so the README diffs are larger than the two added people. Worth confirming that `muzimu217` should be on the wall — this PR includes them deliberately.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Documentation and generated contributor assets only; no runtime or security-sensitive code paths.
>
> **Overview**
> **Regenerates the bilingual community contributor wall** (18 → 20 people) via `scripts/update_contributors.py`, with no application code changes.
>
> Adds **CyrusAuyeung** and **muzimu217** to the avatar set and to the `CONTRIBUTORS` blocks in `README.md` and `README_zh.md`. Existing entries are **reordered** to match current GitHub commit ranking, so the diff looks larger than the two new names. The auto-maintained file tables in `.github/contributors/README.md` and `README_zh.md` gain rows for the new PNGs.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 93fdfdd2ec8161c409422a9285dee6c315d3238d. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f737a0aee691`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.