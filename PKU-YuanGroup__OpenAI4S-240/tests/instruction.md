# Issue

**Title:** docs: refresh Community Contributors and credit brainsparker

## Description

## Summary

The Community Contributors wall omitted @brainsparker even though the You.com search integration in #232 was merged.

Regenerate the English and Chinese README walls from the current GitHub contributors graph and the existing public-recognition list: 24 contributors, including @brainsparker, in the generator's current ordering. Add the new local avatar, refresh the two existing avatar files updated by the generator, and synchronize both avatar-directory inventories.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [ ] Tests / harness / CI
- [x] Docs

## Change Type

- [ ] Bug fix
- [ ] Feature
- [ ] Refactor
- [ ] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
python3 scripts/check_directory_readmes.py
  197 maintained directories, 1999 direct files/assets: complete bilingual coverage

.venv/bin/python -m pytest tests/test_update_contributors.py
  33 passed

git diff --check
  passed

Installed pre-commit hook during git commit:
  EOF, mixed-line-ending, whitespace, merge-conflict checks and mypy passed;
  hooks with no matching files skipped.
```

Manual checks: both root README blocks are identical and contain the same 24 unique contributors; all 24 local PNGs decode as 256 × 256 RGBA images with transparent corners; both avatar inventories match the linked files. Document edits are confined to the generated wall and inventory blocks.

Not run:

```text
Full offline pytest suite
pre-commit run --all-files
Browser/runtime smoke tests
```

Reason:

```text
This change only refreshes generated Markdown and public contributor avatars.
The generator, application code, dependencies and CI workflows are unchanged.
Full PR CI remains responsible for its independent gates; no result from the
previous main-branch run is claimed as validation of this PR's head.
```

## Risk and Reviewer Focus

Low risk: contributor attribution, profile links and avatar rendering. Review the @brainsparker entry against #232, parity between the two root README blocks, and the three changed PNGs. No application or generator behavior changes.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff, including PNG format/dimension checks.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`, `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. (Not touched.)
- [x] Workbench changes were made in `frontend/` and built assets committed where applicable. (No workbench changes.)
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test. (No such changes.)

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site. (No import changes.)
- [x] New dependencies, if any, are documented and justified. (None added.)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual verification notes. (No security-sensitive changes.)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected.

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Documentation and contributor attribution only; no application, API, or security behavior changes.
>
> **Overview**
> Refreshes the **Community contributors** wall in `README.md` and `README_zh.md` from the current generator output: **24** avatars in the script’s ordering, with **@brainsparker** newly credited on the wall (after #232’s You.com search work).
>
> The bilingual avatar inventories under `.github/contributors/` gain a `brainsparker.png` row; the marked `CONTRIBUTORS` blocks are the only README edits in the shown diff—no runtime or generator logic changes.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit b533526de83e4a77b24176ec66df31bb9f4b1440. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01a232e367d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.