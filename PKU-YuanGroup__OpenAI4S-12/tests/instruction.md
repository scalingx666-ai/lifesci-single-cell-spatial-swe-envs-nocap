# Issue

**Title:** fix(security): use os.path.commonpath for path containment (CodeQL follow-up)

## Description

## Summary

. The `normpath` + `startswith` containment checks for `/static/` serving and the jobs `cwd` were **correct but not recognised** by CodeQL's `py/path-injection` sanitizer model, so alerts #14/#16/#17 stayed open on `main` even though the code rejects traversal. Switch both to `os.path.commonpath((base, target)) != base`, the containment idiom CodeQL recognises. Behaviour is unchanged — verified live: legit files serve (200), `../`/absolute escapes are rejected (403 / "cwd escapes the jobs root"), and no directory is created outside the root.

## Change Type
- [x] Bug fix
- [x] Security-related change

## Verification
```text
uv run pytest                       # 299 passed
uv run pre-commit run --all-files   # black · isort · ruff pass
Live: /static/app.js 200 · /static/../../server/gateway.py 403 · /static//etc/hosts 403
      POST /api/compute/jobs {"cwd":"/tmp/x"} -> "cwd escapes the jobs root" (no dir created)
      POST /api/compute/jobs {} -> running
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5c32df5554b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.