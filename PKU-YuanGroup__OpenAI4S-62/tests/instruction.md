# Issue

**Title:** fix(compute): fail closed in the BYOC confinement probe, and describe the boundary that now exists

## Description

## Summary

`docs/security.md`'s "Remote-compute confinement" row claimed `enforce` refuses `byoc:*` ops "because no host-side boundary exists for the provider helper yet", and that `auto` "runs unconfined". Both stopped being true when `security/byoc_confinement.py` landed. Investigating that divergence surfaced a real fail-open in the helper's own probe.

Two separable commits. A third — a fix for the same `.git` worktree problem in `tests/test_byoc_confinement_scope.py` — was **dropped**, because #56 landed the same fix on `main` first and did it better: it resolves the `gitdir:` pointer outside the boundary and names the real metadata directory, so one uniform assertion covers both layouts instead of branching, and it also handles a worktree whose main repository sits outside `$HOME`. This branch is rebased onto that.

**1. `docs(security,compute)` — describe the boundary that now exists**

`compute/manager.py` wraps the helper in a Seatbelt profile (macOS) or bubblewrap invocation (Linux), and `posture()` reports `state: "active"`, `enforced: true` on a host that can establish one. Verified rather than assumed on macOS 26.x: `available()` → `(True, 'macOS Seatbelt')`; a canary planted in `$HOME` and read from inside a real `wrap()` raises `PermissionError`, as does `os.listdir($HOME)`; `security list-keychains` exits non-zero.

The divergence erred safe — the doc claimed *less* protection than existed — but it misled a reader deciding whether to enable BYOC and contradicted `posture()`'s own `detail` string. Two things the old row did not say and the new one does:

- **the network is NOT isolated** (`network_isolated: false`). Calling a provider's REST API is the helper's whole job, so egress is a separate capability and is not enabled. "The helper is confined" reads to most people as "the helper cannot phone home".
- `enforce` **does** still refuse — but only where no boundary can be established (no `bwrap`/`sandbox-exec`, a failing self-test, an unsupported platform), and on every op rather than only at submit. The old row was right for those cases and merely missing the qualifier.

`docs/compute.md` carried a stronger form of the same claim, and one of its mode bullets was a real behavioural divergence: `off` is no longer "same as `auto` today". `host.compute` keeps its Prototype marking, re-attributed to the reason in `docs/v02-decisions.md` (no named production-grade provider) rather than to a boundary that is no longer unbuilt.

**2. `fix(compute)` — fail closed when the probe verifies nothing**

`_probe_confined()`'s no-anchor netns fallback answered "I could not perform the check" with `True`. `run_oneshot` only calls it when the caller passed `expect_confined`, so that `True` let an unconfined helper go on to read the credential and call the provider having verified nothing. Neither `OSError` was evidence of confinement:

- `/proc/self/ns/net` missing — under the real bubblewrap boundary `/proc` is mounted (`--proc /proc`), so its absence says the process is somewhere *unexpected*, not somewhere confined;
- `/proc/1/ns/net` unreadable — the most reachable way in, since an unprivileged helper whose PID 1 belongs to root routinely cannot stat it.

A malformed `OPENAI4S_HOST_NETNS_INO` also now fails closed instead of raising `ValueError` out of the probe.

**What this does not change:** the macOS branch returns early and never reaches this fallback, and was already fail-closed. No host triggers these paths today, since the manager always supplies the anchor when it wraps. This is about which way the system slides when that stops being true.

`OPENAI4S_HOST_HOME_DEV` is the live anchor and nothing pinned it — the scrub test covered only the legacy netns var, so a `HOST_`-shaped addition to `BASELINE_SECRET_PREFIXES` would have scrubbed the anchor with every assertion still green, dropping the probe into exactly the fallback above. Now pinned.

## Area

- [x] Compute / remote execution
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [x] Documentation
- [x] Security-related change

## Verification

Ran:

```text
uv run pytest tests/test_byoc_confinement.py tests/test_byoc_confinement_scope.py tests/test_compute_nvidia.py
    -> 57 passed, 1 skipped
uv run mypy                        -> Success: no issues found in 6 source files
uv run pre-commit run --all-files  -> all hooks passed
uv run python scripts/check_directory_readmes.py
    -> 100 maintained directories, complete bilingual coverage
uv run pytest                      -> see "Not run" below

Manual, on macOS 26.x (measured, not inferred):
  bc.available()        -> (True, 'macOS Seatbelt')
  bc.posture('enforce') -> enforced=True, state='active', network_isolated=False
  canary planted in $HOME, read from inside a real bc.wrap() -> PermissionError
  os.listdir($HOME) from inside                              -> PermissionError
  security list-keychains from inside                        -> exit 1
  mutation test: reverting the three probe returns makes the new test fail with
    "unverifiable must not report confined"

Re-run after rebasing onto main (which upgraded mypy 1.20->2.3, isort 5->8 and
ruff): targeted tests 57 passed / 1 skipped, mypy clean, pre-commit --all-files
clean under the new pins.
```

Not run:

```text
uv run pytest (full offline suite) — completes except for a pre-existing
  environment gap, unrelated to this change:
    tests/test_admet_genetic.py            -> collection error: No module named 'pandas'
    tests/test_catalyst_sar_screening.py x2 -> RuntimeError: need matplotlib
scripts/capture_response_schemas.py --check -> exits 2, blocked by the same
  pandas collection error ("the suite failed; the capture would be incomplete")
Linux / bubblewrap execution of the BYOC boundary
```

Reason:

```text
The local venv holds only the locked lightweight dependencies, without the
`science` extra, so pandas/matplotlib are absent. Those three failures are
present on the base commit and are not touched by this change; CI installs
what the suite needs. The schema gate is blocked by that same collection
error rather than by drift. (Worth noting for whoever runs that gate next: it
also used to be blocked inside any worktree by the `.git` probe that #56 has
now fixed on main.)

No Linux host, container runtime, or VM was available here, so the bubblewrap
half of the row is supported by code reading and branch simulation (mocked
platform + PATH) rather than by execution. The nightly linux-sandbox-smoke
job exercises OPENAI4S_KERNEL_SANDBOX, not OPENAI4S_COMPUTE_CONFINEMENT, so
the Linux BYOC boundary has no automated proof anywhere today. Flagged rather
than papered over; a harness/smoke/linux_byoc.py alongside the existing kernel
smoke would close it.
```

## Risk and Reviewer Focus

**Lowest confidence: the Linux claims in the `docs/security.md` row.** They are the one part not confirmed by execution — see above. Reviewers with a Linux box should sanity-check `bc.available()` and `bc.posture('enforce')` there.

`_resident.py:_probe_confined()` is the only behavioural change, and it moves a security decision from fail-open to fail-closed. The direction is safe, but it means a host that *cannot* verify confinement will now be refused under `enforce` where it previously proceeded. No current host reaches those paths (the manager always supplies the anchor when it wraps), so no behaviour change is expected in practice.

`compute/manager.py` is a hotspot file; the only edit there is a five-line comment correction, no logic.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched — `manager.py` receives a comment-only change.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets.
- [x] No tests were deleted without tracked replacements (`git ls-files --deleted` is clean).
- [x] The probe change ships focused coverage, including a positive control so the new assertions cannot pass on a probe that only ever returns `False`, plus a mutation check that the test fails against the old behaviour.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded — none added; `_resident.py` remains stdlib-only, as the sandboxed provider runtime requires.
- [x] No new dependencies.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased result is disclosed.
- [x] Security-sensitive changes include verification notes — the canary probe and mutation test above. The `$HOME` canary was synthetic and removed afterwards; the keychain check reads no secret, only whether securityd answers.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees — this PR exists to correct an understatement, and adds the explicit `network_isolated: false` caveat plus the Linux-unproven note above.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs.
- [x] `README.md` / `README_zh.md` sync — not affected. `docs/security.md` and `docs/compute.md` have no per-file `_zh` siblings (only the `docs/README` pair is bilingual, and it already lists both files), so no translation is required; `check_directory_readmes.py` passes.

---

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0276ca5ee3c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.