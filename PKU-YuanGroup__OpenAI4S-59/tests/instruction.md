# Issue

**Title:** chore(deps): declare the dev floors the gate is actually verified against

## Description

Follow-up from the #45…#57 review pass.

Both dev floors currently admit versions that would weaken or break a gate, and **CI cannot catch either**, because every in-repo path goes through `uv sync --locked`. The loose declaration only misleads a contributor who installs from `pyproject.toml` directly — and then gets a weaker check than CI runs.

| declared | becomes | why |
|---|---|---|
| `mypy>=1.14,<3` | `mypy>=2.3,<3` | Dependabot widened the *ceiling* rather than raising the floor when it moved 1.20.2 → 2.3.0 in #50, so the range still admits 1.x — where `local_partial_types` defaults **off**. The strict boundary has only ever been verified under 2.x. |
| `pre-commit>=3.0` | `pre-commit>=3.2` | Two of the pre-commit-hooks hooks (#48) and the isort hooks (#46) now declare `minimum_pre_commit_version: 3.2.0`, which pre-commit validates at manifest load — a hard error, not a skip. The declared floor became unsatisfiable in practice the moment those bumps landed. |

Also adds `local_partial_types = true` to `[tool.mypy]`. It is a mypy 2.x default, so this changes nothing today. The point is that what the strict boundary checks should be readable in the config rather than being a function of which mypy major the resolver produced — the same reason `strict_bytes` is stated explicitly.

## Scope

`uv lock` moves only the two specifier strings in `[package.metadata.requires-dev]`:

```diff
 dev = [
-    { name = "mypy", specifier = ">=1.14,<3" },
-    { name = "pre-commit", specifier = ">=3.0" },
+    { name = "mypy", specifier = ">=2.3,<3" },
+    { name = "pre-commit", specifier = ">=3.2" },
     { name = "pytest", specifier = ">=7.4" },
 ]
```

No resolved version changes — mypy 2.3.0 and pre-commit 4.6.1 already satisfy the new floors.

## Verification

- `uv run mypy` → `Success: no issues found in 6 source files`, with `local_partial_types` now explicit.
- `uv run pre-commit run --all-files` → every hook passes.
- Nothing in `tests/`, `scripts/` or `harness/` asserts on the declared dev-dependency strings, so the change has no test surface beyond the lock consistency CI already enforces.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `810443a14adb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.