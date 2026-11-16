# Issue

**Title:** Rename local pow() to avoid issue with next Armadillo

## Description

Hi harmony team,

The next release of Armadillo will have a slightly expanded `arma::pow()` function. In `harmony` you flatten the namespace so your local `pow()` helper then gets confused with what (Rcpp)Armadillo will bring.  One possible fix (suggested by Conrad) is to rename your helper; this PR does that.  I tested it first against the release tarball and now against git, and `R CMD check` continues to pass.

It would be helpful to if you could update `harmony` with a simple spot release as we then will not have to discuss 'changes' with CRAN.  We will probably look into releasing a new `RcppArmadillo` within two or three weeks.  You are of course under no obligation to change this, but are likely to then hear from the CRAN maintainers with firmer language <wink>.

Let us know if you have questions.  

Cheers,  Dirk

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6866e01e4d7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.