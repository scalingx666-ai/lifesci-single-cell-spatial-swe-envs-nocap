# Issue

**Title:** perf: optimization of rank_genes_groups

## Description

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

@ilan-gold replayed changes of #4118 onto main

Edit on 07/15/2026: @ilan-gold I widened the scope of this PR to include two things:
- the stats computation improvements (original focus)
- and added illico's return_as_scanpy

I decided to combine these into one PR because they have some overlap, and I think it would be more cumbersome to have to come back again and do a separate PR review. Especially since rank_genes_groups overall is kinda obfuscated / not pythonic and I'm always losing track of what's going on in this file lol

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8673b4d0a432`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.