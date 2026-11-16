# Issue

**Title:** chore(ci): retire the history secret scan and the Linux sandbox job

## Description

## Summary

Removes two CI jobs. They are removed for different reasons, and only one of them was failing.

**Linux bubblewrap enforcement (nightly) — could never pass.** A GitHub-hosted runner confines unprivileged user namespaces, so `bwrap` creates its network namespace and then cannot bring up loopback inside it:

```
bwrap: loopback: Failed RTM_NEWADDR: Operation not permitted
```

Nothing in this repository can influence that from inside the runner. The job arrived in 6ae9d81, whose subject is *"prove Linux's tier"*, and it failed on **every** scheduled run from that day forward — it never went green once, so it never proved the thing it was named for. A check that cannot pass is not evidence; it is a signal people learn to scroll past.

`harness/smoke/linux_sandbox.py` is **kept** and re-labelled manual — the runner is what cannot run it, not the test. `docs/platforms.md` moves the Linux gate from "**met**, smoke-tested nightly" to "written, not continuously verified", and spells out both the runner limitation and the command to re-establish the claim by hand.

**Gitleaks full-history scan — worked, but costs too much to keep green.** To be clear about the sequencing: this is *not* removed because it was red. #57 had just fixed it, replacing `<commit>:<file>:<rule>:<line>` fingerprints (which squash-only merging duplicates out from under you) with anchored `regexTarget = "secret"` allowlists that survive a rewrite, and the scan has been green since.

It is removed because of the standing cost that fix could not eliminate: a generic entropy rule over all history fires on synthetic fixtures, and a fixture that has to *look* real in order to be found by the code under test is exactly the kind this repository keeps needing. Each one becomes another allowlist row a reviewer must argue for.

**That is not a hypothetical — it happened during this PR.** #57 curated two values; #63 added a third within the day, for a string the working tree already suppressed with an inline `gitleaks:allow`, because an inline comment cannot cover the commit that introduced the line before the comment existed. And the commit #63 names as the source is `d8cef1a` — the first push of *this branch*, where removing that now-dead comment was enough to surface the value again. Each of those suppressions is correct. None of them is free. #57 bought the scan a green run; it could not stop the list from growing.

`scripts/source_secret_scan.py` (already in `ci.yml`, already green) keeps the property that mattered: **named** provider detectors — AWS, GitHub, OpenAI, Google, Slack, Stripe, private keys — instead of entropy. A placeholder in a fixture is not a finding, while a real key in that same file still is, with no list to curate. CodeQL is untouched.

**What this gives up, stated plainly:** a credential that was committed and later removed is no longer detected. Only the working tree is scanned. If that capability is needed again, run gitleaks over history once by hand rather than reinstating a scheduled job with an allowlist to feed. This tradeoff is written into `tests/test_governance.py` and the workflows README so the next person finds the argument instead of repeating it.

This branch has been rebuilt twice on top of gitleaks work that merged mid-flight — first #57, then #63 — so it removes the `.gitleaks.toml` both PRs built, including #63's third allowlist row. It is currently based on 4f5b217.

## Area

- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Security-related change
- [x] Documentation

## Verification

Ran:

```text
uv run pre-commit run --all-files                       # all hooks pass (black, isort, ruff, mypy)
uv run python scripts/check_directory_readmes.py        # 100 dirs, 730 files, complete bilingual coverage
python scripts/source_secret_scan.py                    # passed (957 files)
uv run python -m harness.cli run --tier pr --offline    # 3/3 PASS
uv run pytest tests/test_governance.py tests/test_share_projection.py \
              tests/test_platform_support.py tests/test_release_gates.py   # 51 passed
```

Not run:

```text
uv run pytest            # the full offline suite
```

Reason:

```text
A concurrent worktree on the same machine had it at ~60s per 7 tests, i.e. ~4.5h
to finish. It reached 44% (1653 tests) with 3 failures, each of which was traced
and none involve this change:

  - test_byoc_confinement_scope.py -- git_dir: 'ERR:NotADirectoryError', the
    known "`.git` is a file in a worktree" probe. Already fixed and merged in #56,
    so it does not reproduce on CI.
  - test_followup_admission.py, test_frame_repository.py -- both pass in
    isolation (35 passed); they fail only under the concurrent-run contention.

CI runs the full suite on 3 interpreters, which is this change's first complete
verification. Offline tests (py3.10) has since passed on CI at df91356, the
pre-rebase commit with substantively identical content; the current head
21dcdc5 is re-running all three.
```

## Risk and Reviewer Focus

The risk here is not breakage — no runtime code is touched — it is **reduced coverage**, so review the tradeoff rather than the diff mechanics:

1. **`tests/test_governance.py`** — start here. 4 gitleaks test blocks (116 lines, most of them added by #57) are deleted. They are replaced by one test that pins the *replacement* posture and records why the scan went away, but this is **not** a one-for-one replacement: the assertions about gitleaks' checksum pinning, `useDefault = true`, and the allowlist shape are simply gone, because what they guarded is gone. Decide whether you accept that.
2. **Is losing history scanning acceptable?** That is the real question this PR asks. If the answer is no, the alternative is to keep #57's config and accept curating the allowlist as fixtures accumulate.
3. **`docs/platforms.md`** — verify the Linux tier wording is now *weaker* than what CI proves, not stronger. The old text claimed "**met**" and "smoke-tested nightly" on the strength of a job that was failing every night.

Neither removed job is a required status check (those are `Lint (pre-commit)`, `Offline tests (py3.10)`, `Offline tests (py3.12)`, `Branch naming policy`), so no PR is blocked either way.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: none touched.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [ ] **No tests were deleted without tracked replacements.** — flagged deliberately. 4 gitleaks blocks are deleted and one replacement test is added, but it pins the new posture rather than restating the old assertions. See Reviewer Focus #1.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage: N/A, none touched.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded: N/A, no imports changed.
- [x] New dependencies, if any, are documented and justified: none added.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include verification notes: `source_secret_scan.py` run recorded above; the coverage given up is stated explicitly rather than glossed.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees — this PR exists partly to *stop* `docs/platforms.md` overstating the Linux sandbox guarantee.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs.
- [x] `README.md` and `README_zh.md` stay in sync: both workflow READMEs and both `harness/smoke` READMEs updated together.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f5b217281cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.