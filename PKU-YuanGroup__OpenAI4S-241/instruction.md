# Issue

**Title:** chore: remove automatic reviewers and centralize merge review

## Description

## Summary

Remove `.github/CODEOWNERS` so opening a PR no longer automatically requests area reviewers. Document that the lead reviews and decides when to merge, while contributors can use forks and PRs without direct write access.

Update the bilingual README links and directory inventories, and remove an obsolete maintainer-role comment without changing contributor recognition. Repository settings were separately verified with zero required approvals and Code Owner/additional approval requirements disabled; the existing required checks, resolved-thread requirement, and force-push/deletion protections remain.

## Area

- [x] Docs

## Change Type

- [x] Documentation

## Verification

Local validation at governance commit `b78bbb82` (before syncing the latest `main`); the synchronized head is covered by PR CI:

```text
uv run pytest -n auto --maxprocesses=4 --dist loadfile
  11934 passed, 43 skipped, 2 warnings
uv run pre-commit run --all-files
  passed, including strict mypy
uv run python scripts/check_directory_readmes.py
  complete bilingual coverage
uv run python scripts/source_secret_scan.py
  passed
git diff --check
  passed
```

Not run: browser E2E, frontend rebuild, response capture, and release packaging.
Reason: this change only removes governance configuration and updates documentation/comment text; runtime, routes, frontend, and packaging are unchanged.

Manual checks: verified the live review-rule settings and cleared remaining reviewer requests on open PRs. No reviewers are requested for this PR.

## Risk and Reviewer Focus

Review the deletion of `.github/CODEOWNERS` and `.github/CONTRIBUTING.md`. Review responsibility moves to the lead without requiring an external approval; authors cannot approve their own GitHub PRs. Ordinary contributors retain the public fork-and-PR workflow. Organization-owner access remains inherited and is managed separately.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched (not touched).
- [x] Workbench source/dist requirements are satisfied (no workbench changes).
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway coverage requirements are satisfied (no such changes).

### Core Dependency Policy

- [x] No hard third-party import was added to the core.
- [x] Optional science imports remain guarded (unchanged).
- [x] New dependencies are documented and justified (none added).

### Public Disclosure and Security

- [x] No secrets, credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, or unreleased experimental result is disclosed.
- [x] Governance changes include manual verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual behavior.
- [x] The review-policy changes are documented.
- [x] `README.md` and `README_zh.md` stay in sync.

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Medium Risk**
> Governance-only but shifts merge gating from mandatory area/code-owner reviews to a single lead decision, which weakens enforced multi-reviewer coverage on security-sensitive paths despite unchanged CI requirements.
>
> **Overview**
> This PR **removes** `.github/CODEOWNERS`, so new PRs no longer auto-request path-based reviewers.
>
> **Review and merge policy** is rewritten in `.github/CONTRIBUTING.md`: **Nobody-Zhang** is the lead who reviews and decides when to merge; other reviews are voluntary and not merge-blocking. GitHub is documented as **zero required approvals**, with Code Owner and extra approval rules off, while **required CI** and **resolved review threads** stay in place. Security-sensitive paths still need a **lead security-focused review** (not a separate CODEOWNERS owner). Contributors are directed to **fork + PR without write access**; direct repo grants are limited to the lead.
>
> Bilingual **README** contributing blurbs and **`.github/CONTENTS*.md`** inventories drop `CODEOWNERS` references and describe the new workflow. **`scripts/update_contributors.py`** only updates a comment (no maintainer/CODEOWNERS wording); contributor recognition is unchanged.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 9290f7bf3e86419238a633e85a98b67df5351022. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1134eab883fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.