# Issue

**Title:** ci(docs): gate Pages deploy to master only; build still runs on dev

## Description

## Summary

The docs workflow currently fires on push to both \`master\` and \`dev\` and runs both jobs (build → deploy) on each. That means **any push to \`dev\` silently publishes to www.trimgalore.com**, overwriting whatever master last deployed.

For the post-GA "master = stable, dev = work-in-progress" workflow, this is too permissive — a WIP commit to dev (typo, broken layout, in-flight feature docs) lands on the canonical user-facing URL with no gate.

## Change

Gate the \`deploy\` job on \`github.ref == 'refs/heads/master'\` (or manual workflow_dispatch). Build job is untouched and continues to validate on both branches.

\`\`\`diff
   deploy:
     runs-on: ubuntu-latest
     needs: build
+    if: github.ref == 'refs/heads/master' || github.event_name == 'workflow_dispatch'
     environment:
       name: github-pages
\`\`\`

## Behaviour after this lands

| Trigger | Build | Deploy |
|---|---|---|
| push to \`master\` | ✅ | ✅ |
| push to \`dev\` | ✅ | ⏭ skipped |
| \`workflow_dispatch\` (any branch) | ✅ | ✅ |

Net: dev gets validation safety on docs builds without shipping in-progress content to the live site. workflow_dispatch escape hatch preserved for manual re-deploys.

## Test plan

- [ ] After merge, push a docs-touching commit to dev → build runs, deploy is skipped (visible in Actions tab as "Skipped" on the deploy job).
- [ ] Next push to master (or release-time master FF from dev) → both jobs run, site updates as normal.
- [ ] Manual \`gh workflow run docs.yml --ref dev\` still publishes if you ever want to override (though typically you'd want to FF master to dev first instead).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2773b213bc23`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.