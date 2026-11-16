# Issue

**Title:** Update scverse template to v0.7.0

## Description

## Summary

Manually applies the cookiecutter-scverse v0.7.0 template update, resolving the conflicts and RTD build failure from the automated PR #260.

- **Dependency management**: Migrated from `optional-dependencies` to PEP 735 `dependency-groups`
- **Python support**: Dropped Python 3.10 (minimum now 3.11), test matrix updated to 3.11/3.14
- **GitHub Actions**: Updated checkout (v5), setup-uv (v7), added codecov OIDC auth
- **Documentation**: Switched math rendering from MathJax to KaTeX, updated intersphinx mappings
- **ReadTheDocs**: Updated to Python 3.13 with Node.js support
- **Issue templates**: Migrated from `labels` to `type` field
- **Pytest**: Migrated from `[tool.pytest.ini_options]` to `[tool.pytest]` with `strict = true`

All project-specific values preserved (version 2.1.4, dependencies, URLs, email, etc.).

Supersedes #260 (automated bot PR with unresolvable conflicts and missing source tree).

## Test plan

- [x] `hatch build` succeeds locally
- [x] `hatch env show` correctly parses dependency-groups
- [x] `pyproject-fmt` passes
- [ ] ReadTheDocs preview build passes
- [ ] CI tests pass

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9e9a3fc2dcf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.