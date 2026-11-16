# Issue

**Title:** ci(release): make tag-precheck idempotent when tag matches source-branch HEAD

## Description

## Summary

The \`Check release\` job's tag-precheck currently fails hard on \`Tag \$VERSION already exists\`, cascading to every downstream job (binaries × 3 platforms, Docker × 2 arches, Create-tag-and-release, Upload-binaries, Publish-to-crates.io) being skipped. That's what happened on the v2.3.0 release cycle: after manually running \`git tag v2.3.0 && git push origin v2.3.0\` between the version-bump commit and the \`workflow_dispatch\` trigger, the pretag tripped the precondition, the workflow reported "completed" (with \`conclusion: failure\`), and no binaries / Docker / crates.io actually shipped — even though bioconda's autobump-bot saw the git tag and opened a recipe-bump PR, producing a misleading partial-shipping signal.

Fix: accept a pre-existing tag as safe **iff** it points at the same commit as source-branch HEAD. That covers:
- Accidental pre-tag (root cause of the v2.3.0 incident)
- Re-triggered partial runs where a prior attempt got to Create-tag but not further
- Manual tag-then-trigger workflows that some maintainers may prefer

A pre-existing tag at a **different** commit is still a hard error — that indicates a mismatched release intent (someone's re-tagging a wrong version, or triggering on the wrong branch).

## Mechanism

- New \`check-release.outputs.tag_preexists\` boolean output. \`true\` when the tag exists at the correct commit; \`false\` otherwise.
- \`Create tag\` step now has \`if: … && tag_preexists != 'true'\` — creates the tag only when there's actually a new tag to create.
- New sibling step \`Reuse existing tag (idempotency)\` — runs iff \`tag_preexists == 'true'\`, logs the reuse for audit visibility.
- Header comment updated to document the new behaviour without softening the "prefer NOT to pre-tag" recommendation.

## Diff scope

Single file: \`.github/workflows/release.yml\`. 37 insertions / 7 deletions. No behaviour change to release artifacts, only to the workflow's failure surface.

## Test plan

- [x] YAML parses (\`python3 -c 'yaml.safe_load(...)'\`); all 9 jobs intact; new \`tag_preexists\` output present.
- [ ] After merge to \`dev\`, run \`workflow_dispatch\` with \`dry_run: true\` on a branch that has a pre-existing tag matching HEAD → should complete cleanly with the "Reuse existing tag" step running (verifies the happy path).
- [ ] Run \`dry_run: true\` on a branch where the tag exists at a DIFFERENT commit → should hard-error (verifies the mismatch guard).
- [ ] Next real release (v2.3.1 / v2.4.0) cut from \`master\` after FF from \`dev\` — will use this fix in production for the first time.

## Related

- The v2.3.0 partial-shipping incident is separately resolved: I deleted the orphaned tag and re-triggered the workflow. v2.3.0 is now fully shipped across git-tag / GH Release / crates.io / Docker \`:latest\` + \`:v2.3.0\` / bioconda \`trim-galore = 2.3.0\`.
- The auto-memory \`feedback_release_workflow_trigger\` will be updated in a follow-up commit to add the "don't pre-tag" gotcha + the "check \`conclusion\` not just watch-returned" detection lesson.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `550ab7c5bee8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.