# Issue

**Title:** Modernize Rustfmt conventions and rewrite everything

## Description

Runs a modern version of Rustfmt on the project (the one available via
the `rustup-preview` toolchain in `rustup`) and rewrites a large
majority of the code. This has the nice effect of making everything
quite a bit nicer because it seems that better conventions have won out
in the end.

We also:

* Add a check in CI to make sure new code has been properly fmt'ed.
* Port a few configuration options over from another one of my projects.
  They're benign, and make things a little better.
* Adds a `Makefile` with an `all` target that will conveniently perform
  every important check that will happen in CI.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76dd4bbe65df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.