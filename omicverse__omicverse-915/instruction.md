# Issue

**Title:** fix(synbio): keep rs3 z-scores off the heuristic efficiency scale

## Description

## The bug

`design_grnas(method='rs3')` overwrote `Guide.efficiency` with the Rule Set 3 prediction.

Those are not the same kind of number. rs3 emits a **z-score** — unbounded, routinely negative. `efficiency` is a bounded `[0,1]` GC/poly-T heuristic. Guides too close to the sequence ends to yield a 30-mer context can't be rs3-scored at all, so they kept their heuristic value — and the single `sort` at the end then ranked the whole pool across two incompatible scales.

Concretely, on the target added in this PR (21 SpCas9 guides, 2 of them end-adjacent):

```
+@  1 eff=0.910 rs3=None
-@  5 eff=0.950 rs3=None     <- highest heuristic score in the pool
... 19 guides with rs3 in [-9.5, -0.5]
```

Every scored guide is negative, so **both unscorable guides sorted to the top** — including the one at `eff=0.950`, which took rank 0 ahead of everything the model actually looked at. Asking for the better model made the ranking worse.

## The fix

- `Guide` gains `rs3_score: Optional[float] = None`.
- `efficiency` now always means the heuristic in `[0,1]` and is never overwritten. `crispr_regulation` already relies on this when it computes `score = window_score * efficiency` (`_editing.py:234`) — with a negative z-score in there the product inverts. It happens not to pass `method='rs3'` today, so it was never hit; the invariant is now explicit rather than incidental.
- `method='rs3'` ranks by `rs3_score`; guides that can't be scored rank **last** instead of being interleaved. `top_n` applies after that sort.
- No flanking sequence is invented to manufacture a 30-mer — an unscorable guide is reported as unscored, not guessed at.
- `__repr__` shows rs3 only when present.

Callers who want the old single-number behaviour read `rs3_score`; callers who want a bounded score read `efficiency`. Neither is silently the other.

## Tests

12 tests added to `tests/test_synbio_crispr.py` (the module #914 created), which the `CRISPR + extra guards` CI step already runs. **21 passed** in that module.

`_rs3.predict_rs3` is stubbed, so `ensure_rs3()` never runs: no `--no-deps` pip fetch, no ~20 MB model download, no lightgbm import. The stub deliberately returns **negative** z-scores — that is the regime real Rule Set 3 produces and the one that broke sorting, so a stub returning `[0,1]` values would not have caught this.

Checking out the pre-fix `_crispr.py` under the new tests gives **7 failed / 14 passed**, and the load-bearing failure is a real assertion rather than a missing attribute:

```
FAILED test_rs3_does_not_clobber_heuristic_efficiency - assert 0.0 <= -0.5
```

Also verified through the public API: `ov.synbio.design_grnas` and `ov.synbio.crispr_regulation` (9 guides, all scores in `[0,1]`).

## Not in this PR

`tests/test_synbio_gpu.py` fails locally with `OSError: [Errno 28] No space left on device` — `OMICOS_SYNBIO_WEIGHTS` defaults under `$HOME/.omicverse/synbio_weights`, which is a 15 GB quota on our cluster, and ESMFold does not fit. Unrelated to this change (layer B, no `_crispr` involvement) and it skips cleanly on CPU CI. Filing separately.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01EEdtfKgHr5pRPtCx5UTePa

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55b7fa007b35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.