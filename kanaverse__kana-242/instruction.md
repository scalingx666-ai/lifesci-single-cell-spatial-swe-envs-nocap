# Issue

**Title:** Fix references to unique factor levels in UI.

## Description

, stemming from some old uses of `__unique__`.

This all fundamentally stems from the fact that the logic in

https://github.com/kanaverse/kana/blame/271f1f1ff84be447c750ff373c8c7cbaf41698df/src/workers/helpers.js#L356-L381

is pretty difficult to follow when considering the opaque output of `summarizeArray`.

I'd suggest moving the source of `summarizeArray` out of **bakana** and into this file, to avoid future surprises from misunderstandings of the `summarizeArray` output.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `271f1f1ff84b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.