# Issue

**Title:** docs(parallel): state why the EOF flush may drop a failed send

## Description

.

The three end-of-stream sends discard the send result while their mid-stream siblings check it, and nothing at the call sites says why that is safe. Two reviewers read the asymmetry as silent output truncation; **it is not** — but the reasoning lives in four separate places and none of them is here. This adds it, and changes no behaviour.

<details>
<summary>Why comments and not code (AI-assisted)</summary>

**The claim in the issue does not reproduce.** I injected a panic into `process_single_batch` for one batch sequence and ran `--cores 4` over 20,000 records (5 batches at `BATCH_SIZE` 4096, so the dead worker's receiver is gone well before the reader reaches its EOF flush):

```
control (no panic):        exit 0, big_trimmed.fq = 20000 records
worker panics on batch 2:  exit 1, no output published, no .partial left behind
```

Every route to a dropped work-receiver is caught upstream of publication: a worker `Err` arrives via the result channel and becomes `first_error`; a panic is caught by `handle.join().is_err()`; and a worker that exits because its own `rtx.send` failed does so only when the main thread has already dropped `result_rx`. The joins run **before** `pending_output.commit()`, so a dropped batch cannot truncate a published file.

**Matching the siblings' `is_err()` shape was my first plan and it is not available.** Sites `:715` and `:755` `break` immediately after the flush, so a check there is a literal no-op; `:1205` is at the end of its function with nothing to break out of. Propagating from the reader thread would be actively worse: `reader_join_err.or(first_error)` (`:309`, `:1045`) prefers the reader's error precisely because the worker's carries the full anyhow chain, so a reader-side error here would **mask** the real diagnosis.

**One correction to the issue's framing:** the mid-stream sites do not "surface" the error either. They `break`, and the error arrives via the worker's own report — the `.is_err()` there is an early exit, not a diagnostic. So the checked/unchecked contrast is not detected-versus-undetected.

The neighbouring `tx.send(None)` sentinels are a different case and are left alone: a failed sentinel means that worker had already exited, which is the normal shutdown path.

**Verification.** 803 tests, `fmt` and `clippy --all-targets --release -D warnings` clean. The diff is six added lines, all comments — no test accompanies it because there is no behaviour to test, and I would not add a fault-injection hook to `process_single_batch` for a change with no behavioural effect.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d773131a285d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.