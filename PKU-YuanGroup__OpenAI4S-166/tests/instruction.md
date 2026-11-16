# Issue

**Title:** fix(release): let the guard see the draft; never restage a published version

## Description

## Summary

The first real `publish=true` dispatch for v0.3.0 ([run 35087359578](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/35087359578)) stopped in **guard** with `no release v0.3.0 exists`, although the non-prerelease draft exists. Nothing was published. Every build job in that run passed: quality, distributions, macOS, Linux bundle, Windows package, Windows launcher parse.

- **Guard could not see the draft.** GitHub shows a draft release only to a caller with push access, and the guard used the workflow-level `contents: read` token. The draft-first publish path had never got past this step; its only earlier successful dispatch was v0.2.0's `pypi_only`, which ran against a release that was already public.
  - The guard now holds `contents: write`. It checks out nothing and runs only `gh` and `jq`.
  - A new test requires that every job that looks up the draft (guard, attach, finalize) can see it, and that the guard runs no repository code.
- **Never restage a version PyPI already has.** A second dispatch after PyPI succeeded goes wrong like this:
  1. The rebuilt bytes differ from the published ones, because the build is not reproducible.
  2. `attach` uploads them over the draft's assets (`--clobber`).
  3. The pypi job fails on the reused filename.
  4. `--only publish` then refuses the mismatch, and no retry can finish the release.

  finalize's own recovery comment recommended exactly this re-dispatch. Now:
  - In publish mode, the guard asks PyPI first and continues only on a definite 404.
  - The comment says "Re-run failed jobs" on the same run, which agrees with `docs/release-validation.md`.
  - A test runs the guard's own shell step with a fake `gh` and `curl`.
- **The sealed evidence report no longer claims success early.** `step_evidence` runs before checksums, draft, upload and publish, but it sealed `ok: true` and `published: true` with all 13 steps planned. That bundle is attached to the release and kept for 90 days even when a run later fails. The sealed report now records this invocation's plan, `ok: null`, `published: false` and `sealed_at: "evidence"`.

These defects came from a review of the never-executed publish path: three independent lenses, and each finding checked by a separate agent trying to refute it. Two reported defects were refuted and are not changed:
- finalize's single PyPI lookup (PyPI's shield does not serve stale content);
- the GITHUB_TOKEN PATCH for `--draft=false` (the draft's `target_commitish` is `main`).

Not changed, by maintainer decision: the `pypi`/`ghcr` environments stay without reviewers, as for v0.2.0.

## Area

- [x] Tests / harness / CI
- [x] CLI / config / packaging

## Change Type

- [x] Bug fix
- [x] Release / packaging

## Verification

Ran:

```text
uv run pytest -n 4 tests/test_release_gates.py tests/test_release_pipeline.py tests/test_release_gate_manifest.py \
  tests/test_release_docs.py tests/test_ci_gate_independence.py tests/test_plan_crosswalk.py   -> all passed
mutation checks (each change confirmed to have landed, then reverted):
  guard permissions from main          -> "guard reads the draft with a token that cannot see it"
  PyPI stop removed                    -> test_the_guard_refuses_to_stage_a_version_pypi_already_has fails
  PyPI stop fail-open on non-200       -> same test fails (503 / unreachable cases)
  sealed report back to a verdict      -> test_the_sealed_report_is_a_snapshot_not_a_verdict fails
uv run pre-commit run (changed files); python scripts/source_secret_scan.py
live: run 35087359578 failed only in guard (log: "release not found"); all build jobs green
```

Not run:

```text
a real publish; the full offline suite locally for this diff
```

Reason:

```text
Publishing is the next step, and it needs this merged and the v0.3.0 tag moved. The change is confined to release.yml, release_pipeline.py and their tests, which pass; CI runs the full suite.
```

## Risk and Reviewer Focus

- The guard's token can now write repository contents, but the job runs no repository code.
- If pypi.org is unreachable, the guard refuses to stage (fail closed). Re-dispatch once PyPI answers.
- PyPI's CDN caches a 404 for a missing version briefly (about 60 s), and a cache-busting query string did not bypass it in a live check. So the guard's lookup is a safety net against a mistaken re-dispatch minutes or days later, not against one fired within a minute of the upload.
- The review of the live run also confirmed that every artifact name matches what attach, pypi and finalize download, that the draft has no leftover assets, and that the quality job attests only after about 42 minutes of local gates. That last point means a dispatch should wait until push CI at the release SHA has finished, as this one did. Follow-ups not changed here: evidence and receipts from a failed run are not uploaded; the quality receipt records no platform-check rows; attested rows carry the check-suite id as `run_id`; the contract gate's log prints a runner-local daemon URL.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Medium Risk**
> Changes release CI guard permissions and fail-closed PyPI pre-checks; incorrect PyPI availability could block staging, but scope is limited to release workflow and evidence reporting.
>
> **Overview**
> Fixes three release-pipeline defects that blocked or misrepresented v0.3.0’s first real publish.
>
> The **guard** job now has `contents: write` so `gh release view` can see an existing draft (read-only tokens reported “not found”). In normal **publish** mode it also queries PyPI and only allows staging on HTTP **404**, blocking a second dispatch after the version is on the index—avoiding `--clobber` uploads of non-matching rebuild bytes and stuck half-published state. **finalize** comments and **release-validation** docs now say to re-run failed jobs on the same run, not dispatch again.
>
> **Evidence sealing** in `release_pipeline.py` uses this run’s `planned_steps()` and marks sealed `release-report.json` as a pre-upload snapshot (`ok: null`, `published: false`, `sealed_at: "evidence"`) instead of claiming success before upload/PyPI.
>
> New tests assert draft visibility permissions, execute the guard shell step with fake `gh`/`curl`, and verify the sealed evidence zip contents.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit cd908f9ef272116235c3df8ca5a90bc6ea0885dd. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb3a212529aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.