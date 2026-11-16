# Issue

**Title:** Make the scarf-single-cell skill discoverable

## Description

## Summary

Changes are limited to `skills/scarf-single-cell/`; no package code is touched. The skill now works
when installed outside this repository (skills.sh, SkillsMP and other skill catalogues), and three
recipes no longer crash on common inputs.

## Changes

**Portability**
- The install line is now `pip install "scarf[extra]>=1.0.0rc17"`. A bare `scarf[extra]` installs
  0.32.3, whose API the skill does not describe.
- Repository paths (`docs/source/...`) are replaced by readthedocs links, `uv run` is no longer
  assumed, and headless plotting uses `matplotlib.use("Agg")`.
- `scripts/inspect_store.py` gets a shebang and the executable bit.

**Corrections**
- Converter memory refusals: 1.0.0rc18 and rc19 raise a plain `MemoryError`. `CountLayoutMemoryError`
  only exists after rc19. Fixed in `data-access.md` and the troubleshooting table.
- New troubleshooting row for the cell-cycle gene mismatch on stores without gene symbols.
- `metadata.version` bumped from 0.3 to 0.4.

**Recipe fixes** (each failure reproduced, then the fixed recipe rerun as written)
- `quality-control.md`, removal audit: genes missing from the store are dropped from the marker
  panel, groups that need a missing gene are skipped, and MALAT1 is optional. Previously mouse and
  Ensembl-ID stores raised `KeyError`.
- `integration-and-comparisons.md`, `exact_tests`: a population with fewer than 2 donors in a group
  is reported but not tested, and BH covers only the tested rows. This matches
  `run_statistical_testing`. Previously SciPy raised `ValueError` for n = 1, and the BH step raised
  for n = 0.
- `data-access.md`, H5AD import: only obsm and obs keys that exist in the file are passed.
  Previously a missing key raised `KeyError`.

## Testing

- `skills-ref validate skills/scarf-single-cell` passes, and every readthedocs link returns 200.
- QC audit run on the 1K PBMC (human) and 4K pancreas (mouse) test datasets.
- Donor tests run on synthetic 3 vs 3, 1 vs 3 and 0 vs 3 donor tables.
- H5AD import run on the pancreas file, a copy without `X_umap`, and a modern AnnData copy.
- `npx skills add NygenAnalytics/scarf --list` finds the skill.
- No tests read the skill files and no package code changed, so the test suite was not rerun.

## Maintainer steps after merge

1. **Add the repository topics (needs the Maintain or Admin role).** Topics are repository settings,
   so this PR cannot set them. SkillsMP indexes repositories tagged `claude-skills` or
   `claude-code-skill`, and `agent-skills` is the topic GitHub's own `gh skill` tooling uses:
   ```bash
   gh repo edit NygenAnalytics/scarf \
     --add-topic claude-skills --add-topic claude-code-skill --add-topic agent-skills
   ```
   Or use the gear icon next to "About" on the repository page. SkillsMP syncs daily.
2. **Seed the skills.sh listing with one install.** skills.sh has no submission form. It lists a
   repository once the skills CLI reports an install, so install the skill once with telemetry
   enabled (do not set `DISABLE_TELEMETRY` or `DO_NOT_TRACK`):
   ```bash
   npx skills add NygenAnalytics/scarf --skill scarf-single-cell -g -a claude-code -y
   npx skills remove --global scarf-single-cell   # optional, if you don't want to keep it
   ```
   Replace `claude-code` with the agent you use. The page should then appear at
   https://skills.sh/nygenanalytics/scarf. skills.sh publishes no minimum install count, so it may
   take a while to show. Install it only once; repeated installs just inflate the ranking.

3. **Optional, later:** once https://skills.sh/nygenanalytics/scarf exists, add the badge to the
   README:
   `[![skills.sh](https://skills.sh/b/NygenAnalytics/scarf)](https://skills.sh/NygenAnalytics/scarf)`

Outside this PR: the README's Install section (`uv pip install --python .venv "scarf[extra]"`)
installs 0.32.3. It needs `--prerelease allow`, like the banner above it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `760504c36899`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.