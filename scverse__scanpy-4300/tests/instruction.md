# Issue

**Title:** docs: remove stale `proceed` parameter docs from `tl.draw_graph`

## Description

draw_graph's docstring documents a `proceed` parameter, but it is not part of the function's actual signature. Git history shows that it used to be a real parameter (proceed: bool, optional) and was later removed from the code, but the docstring was not updated.

I found this through numpydoc.validate() and confirmed that this is a genuine documentation drift, rather than the shared {show_save_ax}-style doc template used elsewhere in the plotting module, where parameters like ax are intentionally documented even though they are passed through **kwds.

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our workflow and speed up review.
-->

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] Tests included or not required because: documentation-based change
- [x] Release notes not necessary because: documentation-based change

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ab45dc1d465`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.