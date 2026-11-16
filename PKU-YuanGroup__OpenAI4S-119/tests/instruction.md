# Issue

**Title:** fix(kernel): make the interrupt SIGINT actually land — tgkill the main thread, reset inherited SIG_IGN at spawn

## Description

## Summary

`Kernel.interrupt()` sends one SIGINT and reports it delivered. This PR fixes the two independently verified ways that signal could then be **silently discarded** — one per platform mechanism — plus the test-side timing defect that had been masking them. The two fixes compose: tgkill aims the signal at the right thread, and the spawn-boundary reset guarantees that thread has a disposition that can receive it (tgkill into an inherited SIG_IGN is still discarded).

**1. A helper thread eats the process-directed signal (Linux) — `0573711`**

`test_sigint_interrupt_reports_interrupted_true_lineno_none` failed the **Frozen response shapes** job on the last two `main` pushes (runs 32707873426, 32727066434): worker alive, SIGINT handler installed, nothing pending, cell still running — a remainder the a3b12f5 latch fix could not explain. A branch-only CI reproducer settled it ([run 32735586388](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/32735586388), round 15): the guard phase's `import matplotlib` starts OpenBLAS's pool, those threads inherit an empty signal mask, and Linux may hand a process-directed SIGINT to any of them. CPython's Python-level handler runs only on the main thread, and a main thread blocked in `time.sleep`'s `clock_nanosleep` is never woken by a flag another thread set:

```
tid=2623 MAIN  State: S  SigPnd: 0  SigBlk: 0  wchan: hrtimer_nanosleep
tid=2627/28/29 State: S  SigPnd: 0  SigBlk: 0  wchan: futex_do_wait   (BLAS pool)
round 15: eventually interrupted=True wall=30.0005   ← the stop did nothing until the sleep expired
```

Fix: `Kernel.interrupt()` aims `tgkill(pid, pid, SIGINT)` at the worker's **main thread** on Linux (main-thread tid == pid, so no `/proc` read; R's `sh -c 'exec …'` spawn keeps the same equality). A thread-directed signal cannot be consumed by a helper thread — the race is removed, not narrowed. Syscall numbers are stable per-arch ABI (x86_64: 234, aarch64: 131); any other platform/architecture or a failed syscall falls back to the process-directed `Popen.send_signal` exactly as before.

**2. An inherited SIG_IGN makes the R worker born uninterruptible — `e9a8f5a`**

A daemon launched as a shell background job (`./start.sh &`, `nohup openai4s serve`) runs with SIGINT/SIGQUIT set to SIG_IGN, and SIG_IGN — unlike a handler — survives every exec in `daemon → [bwrap] → sh → Rscript`. R follows the classic Unix idiom and installs its interrupt handler only when the inherited disposition is not SIG_IGN, so the R worker discarded every stop in the child (lldb on the stuck worker: `sigaction(SIGINT)=SIG_IGN`, `R_interrupts_pending` stayed 0) while every caller reported a delivered one. Python workers survived only because `worker.py` calls `signal.signal()` unconditionally.

Fix: `PipeTransport.__init__` passes a `preexec_fn` that resets SIGINT and SIGQUIT to SIG_DFL between fork and exec — the one local spawn site every Python, R and bwrap-wrapped worker passes through, so the Linux pidfd delivery target inherits the corrected disposition too. The daemon's own disposition is untouched (an operator who backgrounded it chose those semantics). The alternatives fail structurally: `trap - INT` in the sh wrapper is a no-op exactly when needed (POSIX forbids a non-interactive shell from resetting a signal ignored on entry), and R exposes no supported way to force its handler in. `preexec_fn`'s `signal.signal` is legal off the main thread because CPython runs `PyOS_AfterFork_Child()` first; a regression test pins that from a non-main-thread spawn, where the daemon actually spawns. Other spawn planes were audited: compute-local Popens are kill/deadline-controlled and never signalled INT, the remote compute resident and the daemon's SIGTERM handler are installed unconditionally.

**3. The R interrupt test raced interpreter startup — `8cbacb5`**

The interrupt-drain test armed `threading.Timer(1.0, kernel.interrupt)` against a flooding cell; a conda Rscript can take >2.5 s to start, so the SIGINT landed before the first byte — outside r_worker.R's protected loop it halted the interpreter, inside it it interrupted a cell whose `stdout_seen_bytes` was legitimately 0. Both are startup races, not the mid-stream case under test. The interrupt is now armed from `Kernel.execute(on_chunk=…)`'s first drained chunk (fired after `seen` is bumped, one SIGINT only), so it provably lands mid-stream on any interpreter. `tests/fixtures/fake_rscript.py`'s SLEEP now emits a `stdout_chunk` to arm against — and because CPython honours an inherited ignore exactly like R, the fake reproduces the SIG_IGN drop faithfully on machines without R. The Linux bwrap interrupt smoke now runs entirely under SIG_IGN, proving the backgrounded-daemon chain end to end over pidfd.

**4. Crosswalk re-record — `edc21e7`**: rows R2/P1-03 and R4/P0-3 digest `tests/test_producer_output_budgets.py`, which commit 3 touched; every assertion they rest on is unchanged and the file passes, so only the content digests move (via `scripts/reaudit_crosswalk.py`).

## Area

- [x] Kernel / host RPC / runtime
- [x] Tests / harness / CI

## Change Type

- [x] Bug fix

## Verification

Ran:

```text
# Fix 1 (tgkill), Linux, the failing job's own environment (uv sync --extra science --extra chemistry),
# branch test/sigint-ci-repro:
#   baseline without the fix:  run 32735586388 — 1/80 hangs, with the per-thread /proc dump above
#   with the fix merged:       run 32736701195 — 0/120 hangs under 2-core oversubscription,
#                              tests/test_kernel.py green (includes both new tests)

# Fix 2 (SIG_IGN), macOS, conda r-mini R:
uv run pytest tests/test_kernel.py tests/test_r_kernel.py tests/test_producer_output_budgets.py -q   # 108 passed
uv run pytest -n auto --maxprocesses=4 --dist loadfile      # full offline suite green (after the crosswalk re-record)
# Falsification: removing the preexec_fn line makes the new regression tests fail with the
# original signature (fake sleeps out 30s, interrupted=False); restored → green.
# Product E2E: daemon launched via a real `sh -c '… &'` (SIG_IGN verified), R cell Sys.sleep(60)
# over REST, /kernel/interrupt → interrupted:true, execution-log status "interrupted" after 1.0 s.

# Both, macOS fallback path:
uv run pytest tests/test_kernel.py -q                        # 51 passed
uv run pre-commit run --files openai4s/kernel/manager.py openai4s/kernel/transport.py tests/test_kernel.py
```

Not run:

```text
The Linux bwrap interrupt smoke locally (Linux-only; its CI job runs it, now under SIG_IGN).
The full offline suite was not re-run a second time after the conflict-free assembly of the
four commits onto this branch; this PR's own CI runs the full matrix.
```

Reason:

```text
Fix 1 is confined to Kernel.interrupt()'s local-process branch and Fix 2 to PipeTransport's
spawn; every other path (transport-remote, sandbox/pidfd targeting, non-Linux) keeps its
previous behaviour by construction (False → fallback; disposition reset only in the child).
```

## Risk and Reviewer Focus

- `openai4s/kernel/manager.py` is a hotspot file; the edit is surgical: one module-level helper (`_signal_worker_main_thread`) plus a 2-line insertion in `interrupt()`'s local-process branch, ahead of the unchanged `send_signal` fallback. `tgkill` on a dead pid returns ESRCH → helper returns False → the existing dead-worker reporting path answers, unchanged.
- `openai4s/kernel/transport.py`: the `preexec_fn` runs between fork and exec — it is three `signal.signal` calls, no allocation, no locks; review that nothing heavier ever creeps into it. It applies to the child only; the daemon's own disposition is deliberately untouched.
- The bubblewrap/pidfd sandbox branch keeps process-directed `pidfd_send_signal` (thread targeting needs Linux 6.9's PIDFD_THREAD): it now benefits from the child's corrected disposition, but a BLAS-thread steal inside a bwrap worker remains theoretically possible — if the bwrap interrupt smoke ever hangs with the round-15 signature, that is the follow-up.
- New tests to focus on: the boundary probe (children start with SIGINT/SIGQUIT at defaults even when the spawner ignores them, also from a non-main thread), the SIG_IGN-parent interrupt tests against both the protocol fake and real R, the helper-thread contract test (explicit stand-ins for the BLAS pool, no science deps needed), and the tgkill mechanism test (syscall number + tgid/tid order proven by delivering SIGUSR1 to the test process itself on Linux; fallback asserted elsewhere).

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`, `host_dispatch.py`, `store.py`, `app.js`, `worker.py`, `manager.py`.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted. (`tests/fixtures/fake_rscript.py` gained a behavior — SLEEP emits a started chunk — not a reformat.)

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements. (The drain test's backgrounded-pytest skip is removed because the scenario it skipped is now expected to work, and test_r_kernel.py pins it.)
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server. (ctypes is stdlib, imported lazily inside the Linux-only helper.)
- [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site.
- [x] New dependencies, if any, are documented and justified. (None.)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees. (The pidfd-path residual is stated above rather than papered over.)

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate. (No interface change: stops that already worked keep working; stops that were silently eaten now land.)
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected. (Not touched.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db0767c877d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.