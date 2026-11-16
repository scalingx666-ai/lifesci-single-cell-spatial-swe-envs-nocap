# Issue

**Title:** Fix cmake gmp

## Description

Here are some changes to make the `--gmp` argument work in the install script.

I removed a few other changes before submitting this PR:
- make the install script print the cmake command line
- remove `-Werror`
- remove `-march=native`

At some point I had `-Werror` problems, maybe because gcc-9 found some new errors.  I can't remember.

`-march=native` was causing trouble because different nodes in our cluster support different extended instruction sets.

I used cmake with '-G Ninja' to generate a ninja file instead of a Makefile, and that worked great.

(P.S. If you ever decide that you hate cmake, I recommend taking a look at meson: mesonbuild.com.  I really like it, it seems more readable that cmake, and is quite responsive to any bug reports.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2bde043330a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.