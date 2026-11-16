# Issue

**Title:** Optionally return graph object from cello_probs

## Description

First of all, thank you for your great tool.
This PR adds the possibility to let `cello_probs` optionally return the graph object. The parameter `return_graph` is used for this. This is by default `False`and therefore does not change the original behavior. If it is set to `True` the graph is returned as the third object in addition to `fig` and `ax`.

The background is that I would like to save the graph object in a different format, as well as recolor it if necessary. Also it allows to output all terminal nodes easily, for example.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d375810a0d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.