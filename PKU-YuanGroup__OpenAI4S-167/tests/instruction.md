# Issue

**Title:** docs(benchmark): hold the workflow and case counts where they are stated

## Description

## Summary

Six prose sites and one release floor described the benchmark as **11 workflows
/ 34 cases**. The tree has been **13 / 46** since `21b8bc93`, which added
`codebase-mode` (9 cases) and `delegation` (3 cases) — `tool-bringup`
(`f6e394a6`) was already one of the eleven. `workflows/README.md` and
`tests/test_benchmark_workflows.py` already carried the current numbers.

Review of the first revision (thanks @Nobody-Zhang) found the correction
incomplete and the floor stale. This revision addresses all five points:

1. `README.md:123` — the English feature table still read 11/34 while its
   Chinese sibling was already 13/46, so the pair disagreed. Fixed, article
   included (`a 13-workflow/46-case benchmark`).
2. `scripts/release_import_smoke.py` — `MIN_BENCHMARK_WORKFLOWS = 11` was set
   when the suite had exactly eleven workflows and never raised when
   `codebase-mode` and `delegation` took it to thirteen. `_check_workflow_catalog`
   is the only check that runs against an *installed* wheel, so a wheel that
   lost both newest workflows would still clear it. Raised to 13, and
   `test_installed_release_smoke_floor_follows_the_frozen_catalog` now holds it
   equal to `len(load_workflows())` so the next addition must move it.
3. `openai4s/benchmark/__init__.py:3` — its docstring (what
   `help(openai4s.benchmark)` shows) still said eleven/thirty-four. Corrected.
4. Nothing read the prose counts — which is how 11/34 survived the bump, and
   why the first revision missed `README.md:123` while changing five other
   sites. Added `COUNT_SITES` +
   `test_every_prose_count_matches_the_tree`, following the table-driven gate
   the Skill counts already use in `tests/test_skills_installer_contract.py`.
   The alternation keeps the superseded words so a site that drifts back is
   reported as a wrong value rather than dropping out of the gate.
5. Attribution — corrected in the new commit message and above.

Counted directly from the manifests:

```
$ python3 -c "import json,glob,os; ds=[d for d in glob.glob('workflows/*') if os.path.isdir(d)]; print(len(ds), sum(len(json.load(open(os.path.join(d,'workflow.json')))['cases']) for d in ds if os.path.exists(os.path.join(d,'workflow.json'))))"
13 46
```

`docs/v02-decisions.md:36` deliberately stays out of the new table: it records
the frozen "First 10 workflows / 20 benchmark cases" decision, which is a
statement about the original plan, not a claim about the current tree.

## Area

- [x] Skills / science runtime
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [x] Test / harness
- [x] Documentation

## Verification

Ran:

```text
$ .venv/bin/python -m pytest tests/test_benchmark_workflows.py tests/test_release_gates.py tests/test_skills_installer_contract.py -q
205 passed, 5 skipped

$ .venv/bin/python -m pytest -n auto --maxprocesses=4 --dist loadfile -q
exit 0, zero failures

$ .venv/bin/python -m pre_commit run --all-files
all hooks Passed

$ .venv/bin/python -m mypy
Success: no issues found in 8 source files

$ .venv/bin/python scripts/check_directory_readmes.py
directory docs: 166 maintained directories, 1557 direct files/assets, complete bilingual coverage
```

Negative controls (a new gate that cannot fail measures nothing):

```text
# revert README.md:123 to 11/34 -> "README.md: no sentence matches ... any more"
# change only the number on README.md:286 to `eleven`
#   -> "README.md: says 'eleven' where the tree's workflows count is 13"
# set MIN_BENCHMARK_WORKFLOWS back to 11
#   -> "AssertionError: assert 11 == 13" in the floor test
```

Not run:

```text
Live LLM / GPU / network suites.
```

Reason:

```text
No production behaviour changed; the default offline suite covers this.
```

## Risk and Reviewer Focus

The only behaviour change is the release floor (11 → 13), which makes
`release_import_smoke` **stricter**: an installed wheel must now ship all
thirteen manifests. Worth a look at `scripts/release_import_smoke.py:24` and
the two renamed/added tests in `tests/test_release_gates.py`.

Everything else is prose plus one new test.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose (the counts, and the gates that hold them).
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files (`gateway.py`, `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`) were not touched.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets.
- [x] No tests were deleted without tracked replacements (`test_installed_release_smoke_requires_eleven_workflows` was renamed, not removed).

### Core Dependency Policy

- [x] No third-party import was added anywhere.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, credentials, private data, or local absolute paths are included.
- [x] No unpublished research roadmap or unreleased result is disclosed.

### Docs

- [x] Docs match actual code behavior.
- [x] `README.md` and `README_zh.md` stay in sync.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0484bb1490d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.