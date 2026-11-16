# Issue

**Title:** feat: Add a Github Action that automatically closes stale PRs.

## Description

## Reason for Change

As we move to CI/CD, some automation can help ensure that we're working towards trunk-based development and ensuring that non-draft PRs don't stay open too long without some movement. Ideally, this Github Action helps us with a few things:

1. PRs remain small so that they can be reviewed quickly and merged.
2. If a PR has be alive for more than 2 weeks, updates are required so that there is visibility as to why the PR is blocked. 
3. If the PR has to be alive for more than 2 weeks and is blocked, it reverts to being a draft PR or closed.

## Ticket Number
No ticket.

## Changes

### Additions

Add a Github Action that runs daily. Each day all active (non-draft) PRs older than 2 weeks are marked with a stale tag and a warning comment is made to update the PR. In another 3 days (3 days was chosen to accommodate long weekends + 1 day), the PR will be automatically closed.

### Deletions

None.

### Modifications

None.

## Testing steps

Not tested.

## Notes for Reviewer

None.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ffcf6eb5d842`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.