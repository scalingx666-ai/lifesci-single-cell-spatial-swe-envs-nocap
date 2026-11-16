# Issue

**Title:** Code cleaning

## Description

* add 'use warnings; use strict;' to `fqfilter_v2.pl`
* fix up Perl compile-time errors (mostly variable declarations)
* change file handle approach to use a hash of hashes
* normalise code formatting (e.g. consistent braces / spaces around loops; convert tabs to spaces)
* add SAM file header ()
* explicitly parse arguments in checkPhred method of `distilReads.pm`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3985416cd134`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.