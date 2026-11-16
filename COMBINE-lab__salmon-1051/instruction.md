# Issue

**Title:** perf(infer): profiling harness + optional SQUAREM EM/VBEM acceleration

## Description

# Profiling harness + optional SQUAREM EM/VBEM acceleration

Two additive, **opt-in** performance changes to the EM/VBEM inference path, plus a reproducible profiling harness. **No default behaviour changes**: the shipped binary and default `salmon quant` output are unaffected.

This PR is accompanied by a short literature review, because the acceleration it adds (SQUAREM) is a specific, well-motivated choice from the numerical-optimization literature, and the same review frames the follow-up (#1052, DAAREM).

## 1. Motivation

Salmon estimates transcript abundances with an EM (or VBEM under `--useVBOpt`) over equivalence classes [Patro et al. 2017]. That step is a **fixed-point iteration** `x <- F(x)` that converges only **linearly**, and slowly when the fraction of "missing information" is large, which is exactly the multi-mapping structure of transcript quantification. The cost is paid again for every bootstrap/Gibbs replicate. The goal here is to accelerate the inference **without touching the model** (same fixpoint, same accuracy), plus give us the instrumentation to measure it.

## 2. Literature review: accelerating EM-like fixed-point iterations

**SQUAREM** [Varadhan & Roland 2008] is the accelerator this PR adopts. Treating one EM update as a fixed-point map `F(x)`, from two successive maps it forms difference vectors `r`, `v` and takes a squared extrapolation step `x' = x - 2*alpha*r + alpha^2*v`, then one stabilizing EM map. It is genuinely off-the-shelf (you supply only `F`), adds negligible memory, is typically superlinear, and commonly needs 1-2 orders of magnitude fewer EM evaluations on high-missing-information problems. It is also what the original C++ `CollapsedEMOptimizer` used and what the Rust port had left deferred, so this restores parity.

For context on where SQUAREM sits: it uses only the last two iterates. History-based multi-secant methods, **Anderson acceleration** [Anderson 1965; Walker & Ni 2011], its hardened **DAAREM** form [Henderson & Varadhan 2019], and **quasi-Newton EM** [Zhou, Alexander & Lange 2011], can converge faster on higher-dimensional, ill-conditioned problems, at a higher per-iteration cost. A recent survey [Kuroda 2023] finds no universal winner: SQUAREM's advantage is simplicity and near-zero overhead; the multi-secant methods win on the hardest problems. SQUAREM is therefore the right first accelerator to land (safe, cheap, default-off); DAAREM is offered as a follow-up in #1052.

*(The standard model-level levers, equivalence-class collapse [Bray et al. 2016], stochastic collapsed VB/VBEM [Patro et al. 2017], and range-factorization [Zakeri et al. 2017], are already inside salmon; the remaining algorithmic headroom for the inference kernel is the accelerator itself.)*

## 3. What this PR does

### Profiling harness (`build(profiling)`)
- New `[profile.profiling]` (release + line-table debug info, unstripped) so `samply`/`flamegraph` can attribute samples; the shipped `release`/`dist` binaries and the `.cargo/config.toml` target-cpu floor are untouched.
- Per-phase wall-clock via a `PhaseTimer` on a dedicated `salmon::timing` tracing target (index_load / mapping / eff_length_collapse / em_bias / posterior / output). Pure logging, never touches output or determinism.
- A `criterion` micro/convergence benchmark for the EM/VBEM M-step (`crates/salmon-infer/benches/em_step.rs`) over a seeded power-law equivalence-class fixture.
- `scripts/profile.sh` (samply harness; a `sample_data.tgz` smoke tier plus a documented GIAB tier).

### Optional SQUAREM acceleration (`feat(infer)`)
- New `--emAccel <none|squarem>` (default `none`). `squarem` drives an SqS3 cycle in `run_em_counts` that **reuses the existing sharded M-step kernels** as the fixed-point map `F` (two M-steps + a stabilizing third; steplength clamped to `a <= -1`; non-negativity backoff to the plain double-step).
- The plain path is refactored to share one `F` closure but is **byte-identical** to before. The norm/vector math is sequential for run-to-run determinism regardless of thread count.
- Benefits the point estimate and every bootstrap replicate; Gibbs is untouched (it uses no EM M-step).

## 4. Correctness and measurements

Validated on GIAB **NA12878 / HG001** (ENA `ERR356372`) against a GENCODE v50 index:

- **Same fixpoint** as plain EM: on identical (deterministic-mapping) equivalence classes, TPM Pearson ~ 0.99999 with identical total TPM; residual differences are at the convergence-tolerance level on negligible-abundance transcripts. This is why SQUAREM is **not** byte-identical and is therefore opt-in / default-off, existing goldens and `--deterministic` output are unchanged. Unit tests assert same-fixpoint agreement (EM and VBEM), mass conservation, and a slow-mixer case.
- **Speed** (measured on a 4M-read-pair GIAB subset): offline EM ~7% faster and a 30x bootstrap ~7% faster. The bigger gains show up on slow-mixing / tight-tolerance problems; the warm-started default EM already converges quickly, so the everyday gain is modest but free.

## 5. Verification

Green under the pinned CI toolchain (1.91.1): `cargo fmt --all -- --check`, `cargo clippy --workspace --all-targets -- -D warnings`, `cargo test --workspace --release`.

Happy to split the two commits into separate PRs if you prefer to review the profiling harness and the SQUAREM change independently.

## References

All confirmed against publisher DOIs; none included on memory alone.

- Anderson, D. G. (1965). Iterative procedures for nonlinear integral equations. *Journal of the ACM* 12(4):547-560. https://doi.org/10.1145/321296.321305
- Bray, N. L., Pimentel, H., Melsted, P., & Pachter, L. (2016). Near-optimal probabilistic RNA-seq quantification. *Nature Biotechnology* 34:525-527. https://doi.org/10.1038/nbt.3519
- Henderson, N. C., & Varadhan, R. (2019). Damped Anderson acceleration with restarts and monotonicity control for accelerating EM and EM-like algorithms. *Journal of Computational and Graphical Statistics* 28(4):834-846. https://doi.org/10.1080/10618600.2019.1594835
- Kuroda, M. (2023). Acceleration of the EM algorithm. *WIREs Computational Statistics* 15(4):e1618. https://doi.org/10.1002/wics.1618
- Patro, R., Duggal, G., Love, M. I., Irizarry, R. A., & Kingsford, C. (2017). Salmon provides fast and bias-aware quantification of transcript expression. *Nature Methods* 14:417-419. https://doi.org/10.1038/nmeth.4197
- Varadhan, R., & Roland, C. (2008). Simple and globally convergent methods for accelerating the convergence of any EM algorithm. *Scandinavian Journal of Statistics* 35(2):335-353. https://doi.org/10.1111/j.1467-9469.2007.00585.x
- Walker, H. F., & Ni, P. (2011). Anderson acceleration for fixed-point iterations. *SIAM Journal on Numerical Analysis* 49(4):1715-1735. https://doi.org/10.1137/10078356X
- Zakeri, M., Srivastava, A., Almodaresi, F., & Patro, R. (2017). Improved data-driven likelihood factorizations for transcript abundance estimation. *Bioinformatics* 33(14):i142-i151. https://doi.org/10.1093/bioinformatics/btx262
- Zhou, H., Alexander, D., & Lange, K. (2011). A quasi-Newton acceleration for high-dimensional optimization algorithms. *Statistics and Computing* 21(2):261-273. https://doi.org/10.1007/s11222-009-9166-3

*AI-assisted-research disclosure: the literature search underlying this review was conducted with AI research agents; every reference was verified independently against its publisher DOI, with no fabrication or mashups.*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66f3d3cdaeb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.