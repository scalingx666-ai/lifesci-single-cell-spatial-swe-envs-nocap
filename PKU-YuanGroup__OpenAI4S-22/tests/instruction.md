# Issue

**Title:** feat(scope): add-catalyst-discovery

## Description

<!--
Thanks for contributing to OpenAI4S.

Keep PRs small, focused, and reviewable.
Branch naming: feat/<name>, fix/<name>, docs/<name>, test/<name>,
refactor/<name>, chore/<name>, ui/<name>, harness/<name>, science/<name>,
release/<name>, hotfix/<name>.

OpenAI4S is a public repository. Do not include secrets, private data,
unpublished research plans, internal assignments, or unreleased results in
the PR title, description, branch name, commit messages, code, logs, or tests.
-->

## Summary

Add a new material skill `catalyst_sar_screening` for M-graphene structure–activity
screening locked to FAIRChem UMA (`uma-s-1p1`, task `oc20`).

The skill builds POSCARs from an embedded public fixture catalog
(`contcar_catalog.json`), evaluates dissolution / adsorption / ORR metrics via the
`catagent` conda runtime only (no tabular/heuristic fallback), writes report
deliverables under a run workdir, and documents backend pins plus a canonical
example prompt using `<HF_TOKEN_PLACEHOLDER>`. Offline unit tests cover discovery,
readiness gating, catalog use, and a mocked lean pipeline. Demo shells are
synthetic placeholders without unpublished numeric results.

Provenance is noted in `kernel.py`:
https://github.com/ahrehd0506/Catalyst-Design-Agent and
https://github.com/LEDlamar/chem.

Changed paths:
- `skills/catalyst_sar_screening/` (new)
- `tests/test_catalyst_sar_screening.py` (new)

Core changed: no.
New OpenAI4S package dependencies: no (optional science deps live in conda env
`catagent`, documented in `SKILL.md`).
GPU required for live UMA runs: yes (`requirements: [gpu]`).

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [x] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [ ] Bug fix
- [x] Feature
- [ ] Refactor
- [x] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

<!-- Paste exact commands and manual checks. If something was not run, say why. -->

Ran:

```text
cd Forks/OpenAI4S
PYTHONPATH=skills uv run pytest tests/test_catalyst_sar_screening.py -q
uv run isort --profile black --check-only \
  skills/catalyst_sar_screening/kernel.py \
  skills/catalyst_sar_screening/build_example.py \
  tests/test_catalyst_sar_screening.py
uv run black --check \
  skills/catalyst_sar_screening/kernel.py \
  skills/catalyst_sar_screening/build_example.py \
  tests/test_catalyst_sar_screening.py
uv run ruff check \
  skills/catalyst_sar_screening/kernel.py \
  skills/catalyst_sar_screening/build_example.py \
  tests/test_catalyst_sar_screening.py
```

Not run:

```text
uv run pytest
uv run pre-commit run --all-files
Live UMA / FAIRChem evaluation in conda env `catagent` (GPU + HF_TOKEN)
```

Reason:

```text
Default offline suite for this change is the new skill test module (11 passed);
full-repo pytest and pre-commit were not required to validate this skill-only
addition, and pre-commit hook bootstrap previously failed on network fetch of
GitHub hook repos. Live UMA screening needs GPU, HF hub access, and a user
token, so it is intentionally out of the offline CI path; readiness failure is
covered by mocked/unit checks that ask for HF_TOKEN / HF_ENDPOINT instead of
falling back to another calculator.
```

## Risk and Reviewer Focus

- New skill only; no core / gateway / store / WebUI changes.
- Review `skills/catalyst_sar_screening/kernel.py` for the UMA hard-lock
  (`check_uma_readiness` / `require_uma_ready`), deliverables-only agent
  contract, and ImportError guards around optional science imports.
- Review `SKILL.md` for public-safe example prompt (placeholder token only) and
  pinned conda deps (`fairchem-core==2.19.0`, `pandas==3.0.2`,
  `pymatgen==2026.3.23`).
- Confirm demo shells under the skill root stay numeric-empty and are not
  treated as user answers; live outputs must come from `run_pipeline`
  deliverables.
- Confirm `contcar_catalog.json` is a minimal public fixture (graphene /
  pyridineN slabs), not an experimental dataset dump.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `app.js`, `worker.py`, `manager.py`.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site.
- [x] New dependencies, if any, are documented and justified.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2963ecff04f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.