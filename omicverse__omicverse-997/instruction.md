# Issue

**Title:** Fix `claude-review` workflow permissions to allow PR comment posting

## Description

`claude-review` was failing because the Claude action is configured to post review feedback with `gh pr comment`, but the workflow token only had read access to pull requests/issues. This updates permissions so the action can write its review comment.

- **Root cause**
  - Workflow allowed `Bash(gh pr comment:*)` but job token permissions were:
    - `pull-requests: read`
    - `issues: read`
  - Result: Claude run returned `is_error: true` and the job failed.

- **Change**
  - Updated job-level permissions in `.github/workflows/claude-code-review.yml`:
    - `pull-requests: write`
    - `issues: write`
  - Kept all other workflow behavior unchanged.

- **Relevant diff**
```yaml
permissions:
  contents: read
  pull-requests: write
  issues: write
  id-token: write
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3f808643f4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.