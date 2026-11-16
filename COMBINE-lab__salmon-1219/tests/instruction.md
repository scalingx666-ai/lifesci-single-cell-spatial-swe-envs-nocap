# Issue

**Title:** fix(infer): objective-based DAAREM for plain EM; reject DAAREM with VBEM

## Description

DAAREM (`--emAccel daarem`) was broken in two ways. This PR fixes both, makes it a strong accelerator for plain EM, and rejects it under VBEM, where no variant we tried was an accelerator. `--emAccel` still defaults to `none`, so default output is unchanged.

## Problems

1. **Negative iterates** (first commit). The Anderson extrapolation overshoots below zero, and the port kept the result as the next iterate. The run was SRR21186103 against GENCODE v50 (646k transcripts):
   - About a quarter of the coordinates went negative.
   - The loop falsely declared convergence after 534 M-steps, far from the fixed point (Spearman 0.898 against a fully converged EM).
   - 237 fragments were lost to truncation.
2. **A limit cycle under VBEM.** The port followed CRAN `daarem`'s *objective-free* variant, which accepts a step only if the residual ‖F(x)−x‖ doesn't grow. That test works against VBEM:
   - VBEM's sparse prior drives near-identical isoforms to a winner-take-all split.
   - While the losing isoform drains, the residual grows.
   - So the test refused VBEM's own path to the optimum, and accepted only extrapolations that jumped back into the slow region.

   On synthetic and real data this was a deterministic cycle: one run repeated the exact same state every 9,750 M-steps until `maxIter`. Plain VBEM started from the stall point converged in 66 steps. The package's own documentation calls supplying the objective ["preferable"](https://rdrr.io/cran/daarem/man/daarem.html).

## Changes

- **Floor projection.** The extrapolation is floored at 0.1× the current value, with an absolute floor of 1e-10 so it can never reach exactly zero. Without the absolute floor, 13 transcripts with real support (one with 148 reads at the optimum) underflowed to 0 on a cerebellum run, where EM can never revive them, leaving the answer 0.21 nats short.
- **Objective-based acceptance,** following CRAN's `daarem_base_objfn`:
  - A step is accepted unless it lowers the objective by more than 0.01, with the reference's cycle-level check at each restart.
  - The objective is the log-likelihood for EM, and for VBEM the evidence lower bound (ELBO) at the current Dirichlet.
  - It costs no extra pass over the equivalence classes. Each M-step kernel already computes every class's denominator, so with a compile-time flag it also returns Σ nₖ·ln(denominator).
  - With the flag off, the kernels are unchanged: plain and SQUAREM iteration counts match the previous build exactly on all three datasets.
- **Stopping rule.** DAAREM stops only when salmon's max-relative-difference test passes both between successive iterates and between the iterate and one plain M-step from it. Each check alone was fooled on a test fixture:
  - A brief Anderson stagnation stopped a run 0.66 nats short.
  - Slow mixing stopped another about 30% off.
- **Performance.** The Anderson linear algebra ran single-threaded and cost 3–7× a whole parallel M-step per iteration. It's now chunked, with partial sums added in a fixed chunk order, so it runs in parallel and results still don't depend on the thread count.
- **DAAREM is plain-EM only.** Requesting it with VBEM fails up front in the CLI with an explanation, via `EmOptions::validate`, and the optimizer refuses it too. The reason is in the next section.

## Results

Three GENCODE v50 datasets (646k transcripts): SRR21186103, cerebellum ERR13232583 and testis SRR11517405. 64 threads.

**Plain EM (`--useEM`):**

| dataset | DAAREM, tol 1e-2 | DAAREM, tol 1e-3 | SQUAREM, tol 1e-4 (reference) |
|---|---|---|---|
| SRR21186103 | 493 steps, 2.3 s, −6.1 nats | 1,199 steps, 5.6 s, −0.11 | 75,195 steps, 231 s |
| cerebellum | 508 steps, 2.0 s, −0.12 | 838 steps, 3.3 s, −0.011 | 70,215 steps, 153 s |
| testis | 229 steps, 1.3 s, −16.1 | 853 steps, 4.6 s, −0.053 | 80,271 steps, 313 s |

Nats are log-likelihood relative to the SQUAREM 1e-4 reference. For comparison, plain EM at the default tolerance takes 4–6 s and stops 75–126 nats short.

**VBEM (the default optimizer):**
- **Slower at the default tolerance.** Even the objective-based DAAREM is 1.2–2.4× slower than plain VBEM in wall time: it takes about as many steps, and each step costs more.
- **Doesn't converge at tighter tolerances.** At 1e-4 it hit the 100k-step cap on 2 of 3 datasets.
- **The cause is VBEM's objective.** With the sparse prior it has many optima, and Anderson steps can move between their basins.

SQUAREM remains available with VBEM. It's slightly slower than plain VBEM at the default tolerance, but 1.3–2× faster at matched accuracy.

## Tests

`cargo test -p salmon-infer` (31 tests) and the salmon-cli tests pass; clippy and fmt are clean. New tests check that:
- the objective never decreases under plain EM or VBEM steps, and equals the directly computed EM log-likelihood;
- DAAREM stops as close to the EM optimum as plain EM at the same tolerance, in far fewer steps;
- DAAREM's untruncated output stays non-negative;
- DAAREM with VBEM is rejected.

The existing thread-count determinism test still covers DAAREM.

## Release note

> `--emAccel daarem` is now supported only with plain EM (`--useEM`/`--meta`), where it is the fastest option, typically 30–50× faster than SQUAREM to reach the same log-likelihood. Requesting it with VBEM (the default optimizer) is now an error. Earlier releases could return inaccurate abundances with `daarem`: negative intermediate values and a convergence cycle under VBEM caused premature or false convergence.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `152fa2a84e9e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.