# Issue

**Title:** Issue templates & repo hygiene

## Description

Modernize GitHub issue templates and add dependabot.

## Changes

### Issue templates → YAML forms
- **Bug report**: structured form with report + version info fields (asks for `cellrank.logging.print_versions()` output)
- **Feature request**: single description textarea
- **Question template removed** → redirected to [scverse Discourse](https://discourse.scverse.org/) via `config.yml`
- **`michalk8` removed** from auto-assignees (was on both bug report and feature request)
- Blank issues disabled — forces structured input or Discourse redirect

### PR template
- Removed "search among Pull requests" notice and "How has this been tested?" section
- Kept Description + Closes sections

### Dependabot
- Monthly updates for GitHub Actions (grouped) and pip deps (minor+patch grouped)
- scvelo ignored (version bounds managed manually per scvelo removal plan)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5428e02fad51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.