# Issue

**Title:** feat: support for directed graphs with igraph Leiden clustering

## Description

igraph 1.0 [added a directed variant of Leiden](https://github.com/igraph/igraph/blob/22dd6a8ee4c2b638f769f899cd690f8eff1964d5/CHANGELOG.md?plain=1#L188), so `sc.tl.leiden(flavor="igraph", directed=True)` should no longer raise.

The igraph path in this PR now builds a directed graph except for when `directed=False` is passed (matching the leidenalg path for coherency but it is new behavior for igraph, I can swap interpretation of None if desired).

For directed graphs, scanpy now gives igraph both the outgoing and the incoming edge count of every cell. Given only the graph, python-igraph counts just the edges that leave each cell. With both counts, igraph optimises the same objective as leidenalg's directed modularity.

The `leiden` and `scanpy2` extras now require `igraph>=1.0`, and `leiden` requires `leidenalg>=0.11`, the first leidenalg release that supports it. The igraph release is now more than a year old so I think requiring it should be fine, but should your preference be towards allowing older versions and insteda checking the version inside scanpy, I am happy to adapt this PR.

## LLM usage
- [x] LLM or coding agent used: "Claude Opus 5.5 via Claude Code"
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line

## Checklist
- [ ] Closes #
- [x] Tests: Included, replacing the test that checked that directed igraph raised an error.
- [ ] ~Release notes not necessary because:~

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `117682e1b233`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.