# Issue

**Title:** fix(cli): --skipQuant --deterministic maps and stops (#1140 follow-up)

## Description

Taking note 1 from your #1144 review. Phase 1 sets `skip_quant` for its own purposes (map, write the RAD, do not run the online EM), so the user's `--skipQuant` was overwritten there and never reached phase 2: the run quantified anyway, wrote a full `quant.sf` from a flag asking for no quantification, and then deleted the RAD it had just been asked to produce.

Semantics as you suggested, and as `-a --deterministic --skipQuant` already behaves: take the request before phase 1 overwrites it, run phase 1, stop. The RAD is the deliverable rather than an intermediate, so the keep-condition no longer applies to it.

```
--deterministic              quant.sf written, RAD removed        (unchanged)
--deterministic --skipQuant  no quant.sf, RAD kept                (was: quant.sf written, RAD removed)
```

The test drives the binary, since the bug was in how the two passes were wired rather than in either of them, and asserts both directions: a full run still quantifies and still cleans up, a mapping-only run does neither.

This touches the same handful of lines in `run_deterministic` as #1144, #1147, #1148 and your #1146. Trivial rebase in any order; happy to fold it into whichever of mine you merge last if you would rather have one PR there than two.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4db6f0e3af39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.