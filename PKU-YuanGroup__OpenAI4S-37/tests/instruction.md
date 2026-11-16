# Issue

**Title:** fix: improve Conda environment discovery

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

  Fixes Conda environment discovery to work reliably in more deployment
  scenarios, and bounds package scanning to site-packages directories so
  listing environments no longer walks entire Conda installations.

  Two related issues were fixed:

  1. **Environment discovery missed environments when Conda was not manually
     activated.** The daemon's venv is often created from a Conda Python
     (`sys.base_prefix`), but the discovery path only checked `CONDA_PREFIX`
     and a few hardcoded `~/miniconda3/envs`-style directories. This meant
     environments were invisible unless the caller first ran `conda activate`.

  2. **Packages scanning could take minutes on scientific Conda envs.**
     `pkgscan.py` used `rglob("*.dist-info")` starting from `lib/`, which
     crawled through native toolchains, model caches, and R libraries —
     turning a simple environment listing into a slow directory walk.

  Changes:

  - New `_envs_root_from_prefix()` helper that correctly resolves
    `<base>/envs` from both a base prefix and an activated named
    environment (where the parent *is* the envs directory).
  - Respects `CONDA_ENVS_PATH`, `MAMBA_ROOT_PREFIX`, `CONDA_PREFIX`,
    and `sys.base_prefix` before falling back to hardcoded install
    locations.
  - Tightens `pkgscan._collect_pip` to only scan `lib/python*/site-packages`
    (non-recursive `glob` instead of `rglob`).
  - Adds 4 focused tests covering the new discovery paths and the
    bounded package scan.
  - `.gitignore`: adds `.ruff_cache/`, `.mypy_cache/`, `.venv`.

  ## Area

  - [x] Kernel / host RPC / runtime
  - [x] Tests / harness / CI

  ## Change Type

  - [x] Bug fix

  ## Verification

  Ran:

  ```text
  uv run pytest tests/test_environments.py -v
```

  Not run:



  Reason:

  All 4 new tests exercise the changed discovery and scanning paths
  in isolation (tmp_path + monkeypatch), no live Conda install required.

  Risk and Reviewer Focus

  - _envs_root_from_prefix() in environments.py — the parent-name
  heuristic (path.parent.name == "envs") correctly handles the common
  cases but could misidentify a user-created directory named envs at
  any level. In practice, Conda environments always live at <base>/envs/<name>.
  - pkgscan.py — the glob change from rglob to glob is the
  correctness-sensitive part. It skips packages installed into non-standard
  locations inside lib/, but such layouts are not produced by pip or conda.
  - Discovery order matters. The new checks (CONDA_ENVS_PATH,
  MAMBA_ROOT_PREFIX, CONDA_PREFIX, sys.base_prefix) are inserted
  before the hardcoded home-directory scan, so they take priority.
  Duplicate roots are de-duplicated, so if a path appears in multiple
  sources, the first occurrence wins.

  Checklist

  Diff Readiness

  - [x] I reviewed and understand the full diff.
  - [x] This PR is small and single-purpose.
  - [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
  - [x] Hotspot files were edited surgically if touched: gateway.py,
  host_dispatch.py, store.py, app.js, worker.py, manager.py.
  - [x] openai4s/server/webui/vendor/ and tests/fixtures/ were not
  reformatted.

  Tests

  - [x] Relevant tests or manual checks were run and listed above.
  - [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
  or secrets in the default offline suite.
  - [x] No tests were deleted without tracked replacements.
  - [x] Kernel / host-RPC / gateway changes include focused contract coverage or
  a documented smoke test.

  Core Dependency Policy

  - [x] No hard third-party import was added to the core engine, LLM client, or
  stdlib web server.
  - [x] Optional science imports are guarded by try/except ImportError at every
  in-tree use site.
  - [x] New dependencies, if any, are documented and justified.

  Public Disclosure and Security

  - [x] No secrets, API keys, tokens, real credentials, private data, model
  weights, or local absolute paths are included.
  - [x] No unpublished research roadmap, internal assignment, benchmark detail,
  or unreleased experimental result is disclosed.
  - [x] Security-sensitive changes include appropriate synthetic tests or manual
  verification notes.
  - [x] Docs do not overstate isolation, sandboxing, privacy, or security
  guarantees.

  Docs

  - [x] Docs match actual code behavior.
  - [x] User-facing behavior changes are reflected in docs or release notes where
  appropriate.
  - [x] README.md and README_zh.md stay in sync where translated sections are
  affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e71954465d8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.