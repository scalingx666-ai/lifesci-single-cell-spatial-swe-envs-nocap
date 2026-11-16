# Issue

**Title:** docs: refresh the Community Contributors wall

## Description

## Summary

Refreshes the Community Contributors wall from the live GitHub contributors API by re-running `scripts/update_contributors.py`.

The graph has picked up **`WenyuLiang`** (2 commits), who sorts between `Grace-xyx` and `ClarenceYC` in the commit-count order the wall renders. Every other avatar re-encoded byte-identically, so the diff is exactly one new contributor: a circular PNG plus one row in each root README.

The generator writes the avatar and both root READMEs, but it does not know about the per-directory doc pair, so `.github/contributors/README.md` and its Chinese counterpart get the matching table row by hand — without it `scripts/check_directory_readmes.py` fails on a file the script itself just added.

## Area

- [x] Docs

## Change Type

- [x] Documentation

## Verification

Ran:

```text
GITHUB_TOKEN=$(gh auth token) uv run --with pillow python scripts/update_contributors.py
  -> 17 contributors; circular pngs: 17 refreshed, 17 linked locally; readmes updated: ['README.md', 'README_zh.md']
uv run python scripts/check_directory_readmes.py
  -> 165 maintained directories, 1523 direct files/assets, complete bilingual coverage
uv run pytest tests/test_update_contributors.py -q      -> 7 passed
uv run pre-commit run --files README.md README_zh.md .github/contributors/README.md .github/contributors/README_zh.md .github/contributors/WenyuLiang.png
  -> all hooks passed
file .github/contributors/WenyuLiang.png -> PNG 256x256 RGBA; inspected visually, circular crop with transparent corners
```

Not run:

```text
uv run pytest (full suite)
```

Reason:

```text
The diff is one generated PNG and four Markdown blocks; no Python, frontend,
or packaging file is touched. The generator's own contract test and the
directory-README gate — the two gates this change can actually break — were
both run.
```

## Risk and Reviewer Focus

Effectively zero runtime risk: nothing in the OpenAI4S runtime reads `.github/contributors/`.

Worth a look:
- the new row's position in the wall (commit-count order, ties keep API order), and
- that the same row was added to **both** root READMEs and **both** `.github/contributors/` READMEs, so the translated sections stay in sync.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched (none touched).
- [x] Workbench changes: none.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes: none.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports: unchanged. (Pillow stays a run-time-only requirement of the standalone script, invoked here via `uv run --with pillow`.)
- [x] New dependencies: none.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes: none.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Documentation and contributor assets only; no runtime or application code is affected.
>
> **Overview**
> Adds **WenyuLiang** to the auto-maintained community contributors wall (commit-count order places them between `Grace-xyx` and `ClarenceYC`).
>
> The change inserts one avatar link in the `CONTRIBUTORS` blocks of **`README.md`** and **`README_zh.md`**, and documents **`WenyuLiang.png`** in the bilingual **`.github/contributors/`** README file tables so `check_directory_readmes.py` stays in sync with the generator output.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit c1e325fb52843f2cf6cb9b515674bd721f080f41. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6675117bceec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.