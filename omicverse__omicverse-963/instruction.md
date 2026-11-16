# Issue

**Title:** chore(licences): carry the upstream MIT licences for vendored UCE and SAMap

## Description

`omicverse/llm/UCE/` and `omicverse/external/samap/` hold third-party source copied verbatim, and neither carried the licence that covers it. MIT requires the copyright and permission notice to travel with every copy, so as it stood we redistributed both without meeting that condition.

| Directory | Upstream | Licence |
|---|---|---|
| `omicverse/llm/UCE/` (11 files) | [snap-stanford/UCE](https://github.com/snap-stanford/UCE) | MIT — © 2023 Yanay Rosen, Yusuf Roohani, Jure Leskovec |
| `omicverse/external/samap/` (8 files) | [atarashansky/SAMap](https://github.com/atarashansky/SAMap) | MIT — © 2020 atarashansky |

Both `LICENSE` files are the upstream text verbatim. The `__init__` docstrings now name the source repository and point at the licence beside them. UCE's `__init__.py` was empty, so it also gains the reference and a note that **model weights are distributed separately by the upstream authors under their own terms, which this licence does not cover**.

### Packaging — the part that would have made this cosmetic

A bare `LICENSE` has no file extension, so `MANIFEST.in`'s extension list would have dropped both from the sdist, and with no `package-data` entry they would not have reached the wheel either. The licence would have sat in git and been absent from every `pip install`. Both are fixed, following the entry that already exists for the vendored PDBFixer.

Verified by building the sdist:

```
omicverse-2.3.1/omicverse/external/pdbfixer/LICENSE
omicverse-2.3.1/omicverse/external/samap/LICENSE
omicverse-2.3.1/omicverse/llm/UCE/LICENSE
```

### Not in this PR

A third vendored directory, `omicverse/external/cytotrace2/`, is also missing its licence, but adding it is not the fix. Upstream is the **Stanford Non-Commercial Software License Agreement**, which prohibits use by any commercial entity and directs them to Stanford OTL under docket S24-057. That is an additional restriction, and GPL-3.0 does not permit further restrictions on what it distributes — so dropping the file in would document a conflict rather than resolve one. Handled separately.

This PR is scoped to the two directories where carrying the licence is both necessary and sufficient.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_0156k5ARWtUbtjbfRypRavEa

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a66786954fa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.