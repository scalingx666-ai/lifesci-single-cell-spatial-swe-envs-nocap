# Issue

**Title:** docs(release): v0.3.0 carries an ad-hoc-signed preview macOS image

## Description

## Summary

The v0.3.0 draft release carries `OpenAI4S-0.3.0-macos-arm64.dmg`: built locally from `935b5f2d`, ad-hoc signed, not notarized, and attached by hand rather than by `release.yml`. The repository still says the opposite. Both README halves, `docs/startup-guide.md`, `docs/platforms.md` and the upgrade guide state that v0.3.0 publishes no macOS disk image and send Mac users to PyPI or to the v0.2.0 preview image, and `tests/test_release_docs.py` pins that sentence.

This PR makes the docs describe the release as it is:

- **README.md / README_zh.md** — the macOS note, the v0.3.0 news entry, the startup-guide row and the roadmap item say the image is an Apple Silicon preview (ad-hoc signed, Gatekeeper blocks the first launch) and link the pinned `releases/tag/v0.3.0` page. They do not link `/latest`: a release the workflow produces still carries no image.
- **docs/startup-guide.md** (both languages) — the image section and the Gatekeeper steps now describe the v0.3.0 image, with a checksum command; the v0.2.0 image keeps a one-line pointer. Users coming from the v0.2.0 app are sent to the upgrade guide before the first launch.
- **docs/platforms.md** — still says no release has met the notarization gate; v0.3.0's image is named as a preview attached outside the workflow.
- **docs/upgrading.md / upgrading_zh.md** — the "No macOS disk image" bullet becomes "the image is a preview", with the back-up-first warning for app users.
- **docs/v03-decisions.md** — a new "Amended 2026-09-17" section records the reversal of D11 (v0.3.0). The pipeline's refusal of an un-notarized DMG and the `omit` default are unchanged. **Owner: please read this row; it records your decision in my words.**
- **tests/test_release_docs.py** — the `"v0.3.0 publishes no DMG"` pin is replaced by the preview wording plus its absence, and a new test holds each install doc to naming the image, its pinned page and its signing grade.

**Merge timing:** the links to `releases/tag/v0.3.0` resolve only once the release is public. Merge this when v0.3.0 is published with the DMG attached. If the DMG is removed from the draft instead, close this PR.

## Area

- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Documentation

## Verification

Ran:

```text
uv run pytest tests/test_release_docs.py tests/test_citation_metadata.py        # green
uv run pytest tests/test_benchmark_workflows.py tests/test_cli_catalog_posture.py \
  tests/test_plan_crosswalk.py tests/test_release_gates.py \
  tests/test_skills_installer_contract.py tests/test_schema_migrations.py \
  tests/test_cli_contract.py -n 4 --dist loadfile                               # 417 passed, 3 skipped
uv run python scripts/check_directory_readmes.py                                # complete bilingual coverage
uv run pre-commit run --all-files                                               # all hooks passed
Each new assertion was checked against the base commit's text: all of them fail there.
The DMG itself: scripts/verify_macos_bundle.py passes on the attached bytes
(sha256 1b46e72c…9343; embedded CPython 3.13.13, 38 science packages import, ad-hoc signature).
```

Not run:

```text
The full offline suite was still running locally when this PR was opened; CI runs it.
Browser gates, container smoke, Linux sandbox smokes.
```

Reason:

```text
Docs and one docs-gate test only; no runtime code is touched.
```

## Risk and Reviewer Focus

- The D11 amendment row in `docs/v03-decisions.md` is a decision record. Check that it says what was decided.
- `docs/startup-guide.md` assumes the v0.3.0 app keeps the v0.2.0 layout (`Contents/Resources/runtime/bin/openai4s`, logs in `~/.openai4s/logs/app.out`); both come from `scripts/build_macos_dmg.sh` at `935b5f2d`.
- None of the edited files is a plan-crosswalk evidence file.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: not touched.
- [x] Workbench changes: none.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes: none.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports: none added.
- [x] New dependencies: none.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes: none.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees. The image is described as un-notarized everywhere it is named.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Documentation and doc-gate tests only; no runtime or release pipeline behavior changes.
>
> **Overview**
> Documentation now matches v0.3.0 shipping a **hand-attached, ad-hoc-signed Apple Silicon preview** (`OpenAI4S-0.3.0-macos-arm64.dmg`), replacing text that said there is **no macOS disk image**.
>
> **README** (EN/ZH), **startup-guide**, **platforms**, and **upgrading** guides describe the preview, Gatekeeper on first launch, links to **`releases/tag/v0.3.0`** (not `/latest`), PyPI for Intel or users avoiding un-notarized apps, and backup-before-upgrade when moving from the v0.2.0 app. **v03-decisions.md** adds a **2026-09-17** amendment revising D11 while keeping the release workflow’s `macos_asset=omit` default and refusal to upload un-notarized DMGs.
>
> **tests/test_release_docs.py** drops the “publishes no DMG” pin, asserts preview wording in **platforms.md**, and requires install docs to name the v0.3.0 image, its pinned release page, and ad-hoc signing.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 507e12c9bf7c3458eec8940daf3663b276f5248e. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `935b5f2d5c72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.