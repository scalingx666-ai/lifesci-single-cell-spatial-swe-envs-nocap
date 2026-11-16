# Issue

**Title:** Add GitHub Actions workflow for automated releases

## Description

Creates a workflow that triggers on version tags (v*) to automatically:
- Zip the single-cell-rna-qc skill directory
- Create a GitHub release with the zip file attached
- Generate release notes from commits (as a draft, so we can still manually update then publish)

```
# Create and push a tag
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5707c048074b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.