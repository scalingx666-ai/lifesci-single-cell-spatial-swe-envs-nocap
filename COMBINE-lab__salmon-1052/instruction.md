# Issue

**Title:** feat(infer): DAAREM — a second (opt-in) EM/VBEM accelerator, stacked on #1051

## Description

# DAAREM: a second, opt-in EM/VBEM accelerator

> **Stacked on #1051.** DAAREM reuses the `EmAccel` / fixed-point-map (`F`) infrastructure introduced there, so the first two commits in this PR are #1051's. Please review/merge #1051 first; this PR then reduces to the two `daarem` commits. It is **opt-in and default-off** (`--emAccel daarem`), so there is no change to default behaviour, goldens, or `--deterministic` output.

This PR is accompanied by a short literature review, because the design question ("can salmon's EM/VBEM inference be made faster without changing the model?") has a well-developed answer in the numerical-optimization and RNA-seq literature, and the choice of accelerator follows directly from it.

## 1. Motivation and research question

Salmon pairs a fast mapping stage with a statistical model (EM, or VBEM under `--useVBOpt`) over equivalence classes to estimate transcript abundances [Patro et al. 2017]. The EM/VBEM step is a **fixed-point iteration** `x <- F(x)` that converges only **linearly**; when the fraction of "missing information" is large (exactly the multi-mapping / equivalence-class structure of transcript quantification), plain EM crawls, and this cost is multiplied by every bootstrap/Gibbs replicate.

The question is whether that inference can be accelerated **without touching the model** (same fixpoint, same accuracy). The literature answers yes, and it identifies *which* accelerators to prefer.

## 2. Literature review: accelerating EM-like fixed-point iterations

**SQUAREM** [Varadhan & Roland 2008] is the baseline this repo adopts in #1051. From two successive EM maps it forms difference vectors `r`, `v` and takes a squared extrapolation step `x' = x - 2*alpha*r + alpha^2*v` plus a stabilizing EM step. It is off-the-shelf (you supply only `F`), superlinear, and typically needs 1-2 orders of magnitude fewer EM evaluations on high-missing-information problems. Its limitation, relevant here, is that it uses **only the last two iterates**, discarding longer-history curvature.

**DAAREM** [Henderson & Varadhan 2019] is the method this PR implements. It is **Anderson acceleration** [Anderson 1965; Walker & Ni 2011] over a window of the last `m` residuals (a multi-secant quasi-Newton step), hardened with three additions: a damping factor on the least-squares coefficients, periodic restarts of the history, and epsilon-monotonicity control. In the authors' benchmarks it **matches or beats SQUAREM, with the margin growing on harder, higher-dimensional problems**, precisely because it exploits history that SQUAREM throws away. It keeps SQUAREM's off-the-shelf `F`-only interface.

**Quasi-Newton EM** [Zhou, Alexander & Lange 2011] is the other strong high-dimensional contender: a low-rank secant approximation to the EM map's Jacobian, reported to "rival or surpass SQUAREM" and explicitly designed for genomics-scale optimization. **Plain Anderson acceleration** [Anderson 1965; Walker & Ni 2011] is fast locally but non-monotone and fragile far from the solution; DAAREM is essentially the safe, deployable version. A recent survey [Kuroda 2023] confirms the consensus: no accelerator dominates everywhere, but the **multi-secant/history methods (DAAREM, quasi-Newton) tend to win on higher-dimensional, ill-conditioned problems**, while SQUAREM's edge is simplicity and near-zero overhead.

**Reading for salmon.** Transcript quantification lives in exactly the regime the review flags for DAAREM: 10^5-10^6 transcripts, sparse and ill-conditioned equivalence-class structure. So DAAREM is the literature-motivated next step beyond SQUAREM, and the empirical section below confirms it.

*(For completeness: the standard model-level speed/accuracy levers, equivalence-class collapse [Bray et al. 2016], stochastic collapsed VB and VBEM [Patro et al. 2017], and range-factorization [Zakeri et al. 2017], are already inside salmon; the remaining algorithmic headroom for the inference kernel is the accelerator itself.)*

## 3. What this PR does

- New `EmAccel::Daarem` (`--emAccel daarem`, default `none`). A faithful port of the **objective-free** DAAREM variant (CRAN `daarem::daarem_base_noobjfn`): salmon's EM/VBEM computes no likelihood, so the residual-norm monotonicity control is the natural fit. A proposed Anderson step is accepted only if it does not increase `||F(x) - x||` beyond a shrinking tolerance, otherwise it falls back to a plain EM step.
- Reuses the sharded M-step kernels as `F` (the same closure the SQUAREM path uses), so it accelerates the point estimate **and every bootstrap replicate**.
- The small `nlag x nlag` (nlag = 5) Gram eigenproblem uses a **self-contained cyclic Jacobi routine** and a direct port of `DampingFind` (the ridge-damping Newton search), so there is **no new dependency**. All reductions are sequential for run-to-run determinism regardless of thread count; the expensive per-class M-step stays inside the already-parallel `F`.

## 4. Empirical validation

Measured on GIAB **NA12878 / HG001** (ENA `ERR356372`) against a GENCODE v50 index (~0.5M equivalence classes on a 4M-read-pair subset):

| stage | plain | SQUAREM | DAAREM | DAAREM vs plain | DAAREM vs SQUAREM |
|---|---|---|---|---|---|
| offline EM | 26.2 s | 24.5 s | **17.3 s** | **-34%** | **-29%** |
| 30x bootstrap | 238.6 s | 220.8 s | **170.7 s** | **-28%** | **-23%** |

DAAREM is roughly **4x more accelerating than SQUAREM** here, exactly as the high-dimensional literature predicts.

## 5. Correctness, and an honest behavioural note

- Unit tests assert DAAREM reaches the **same fixpoint** as plain EM and VBEM at a tight tolerance (relative difference < 1e-3), conserves total count, and on a slow-mixer hits the analytic fixpoint in a handful of M-steps; plus a Jacobi-eigensolver spectrum test.
- At **salmon's default tolerance** (`rel_diff_tol = 0.01`), DAAREM's abundances differ from plain EM more than SQUAREM's do (on GIAB, ~0.19% of transcripts differ by > 1 TPM), concentrated on ambiguous / ill-conditioned transcript groups. A controlled experiment indicates the cause is that **plain EM under-converges those transcripts at the default tolerance**: on a controlled ill-conditioned two-transcript case, plain stops at its initialization (a0 = 50000) while DAAREM reaches the true fixpoint (a0 = 25001); and on GIAB, tightening the tolerance measurably increases plain's own EM work (offline EM 26.2 s -> 31.0 s). So DAAREM is converging these harder transcripts **more fully**, not less accurately.
- Caveat I want to be explicit about: I could not produce a perfectly controlled same-equivalence-class "gold" reference on GIAB (the `--deterministic` requant path made isolating the tolerance effect awkward), so the "more fully converged" interpretation is well-supported by two converging lines of evidence (a controlled synthetic case plus the GIAB tolerance-vs-work measurement) rather than airtight.

This is a genuine design call for the maintainers: DAAREM is faster and converges the EM more completely, but its output therefore diverges from the historical plain-EM result more than SQUAREM does. Being opt-in and default-off, it changes nothing unless explicitly requested.

## 6. Verification

Green under the pinned CI toolchain (1.91.1): `cargo fmt --all -- --check`, `cargo clippy --workspace --all-targets -- -D warnings`, `cargo test --workspace --release`.

## References

All confirmed against publisher DOIs; none included on memory alone.

- Anderson, D. G. (1965). Iterative procedures for nonlinear integral equations. *Journal of the ACM* 12(4):547-560. https://doi.org/10.1145/321296.321305
- Bray, N. L., Pimentel, H., Melsted, P., & Pachter, L. (2016). Near-optimal probabilistic RNA-seq quantification. *Nature Biotechnology* 34:525-527. https://doi.org/10.1038/nbt.3519
- Henderson, N. C., & Varadhan, R. (2019). Damped Anderson acceleration with restarts and monotonicity control for accelerating EM and EM-like algorithms. *Journal of Computational and Graphical Statistics* 28(4):834-846. https://doi.org/10.1080/10618600.2019.1594835
- Kuroda, M. (2023). Acceleration of the EM algorithm. *WIREs Computational Statistics* 15(4):e1618. https://doi.org/10.1002/wics.1618
- Li, B., & Dewey, C. N. (2011). RSEM: accurate transcript quantification from RNA-Seq data with or without a reference genome. *BMC Bioinformatics* 12:323. https://doi.org/10.1186/1471-2105-12-323
- Patro, R., Duggal, G., Love, M. I., Irizarry, R. A., & Kingsford, C. (2017). Salmon provides fast and bias-aware quantification of transcript expression. *Nature Methods* 14:417-419. https://doi.org/10.1038/nmeth.4197
- Varadhan, R., & Roland, C. (2008). Simple and globally convergent methods for accelerating the convergence of any EM algorithm. *Scandinavian Journal of Statistics* 35(2):335-353. https://doi.org/10.1111/j.1467-9469.2007.00585.x
- Walker, H. F., & Ni, P. (2011). Anderson acceleration for fixed-point iterations. *SIAM Journal on Numerical Analysis* 49(4):1715-1735. https://doi.org/10.1137/10078356X
- Zakeri, M., Srivastava, A., Almodaresi, F., & Patro, R. (2017). Improved data-driven likelihood factorizations for transcript abundance estimation. *Bioinformatics* 33(14):i142-i151. https://doi.org/10.1093/bioinformatics/btx262
- Zhou, H., Alexander, D., & Lange, K. (2011). A quasi-Newton acceleration for high-dimensional optimization algorithms. *Statistics and Computing* 21(2):261-273. https://doi.org/10.1007/s11222-009-9166-3

*AI-assisted-research disclosure: the literature search underlying this review was conducted with AI research agents; every reference was verified independently against its publisher DOI, with no fabrication or mashups.*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66f3d3cdaeb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.