# Issue

**Title:** Improved ergonomics of `Interactive`

## Description

Small PR.
- [x] added the argument `headless: bool = False` to `Interactive.__init__()`. When `False`, the initializer calls `self.run()`. This is a small ergonomics improvement for the user since `interactive.run()` will be always called, and if for some reasons is not needed (like tests with napari being healess), this is still possible thanks to the new argument.
- [x] the `View` widget is now displayed by default. Reasons: the users will almost always want to show the `View` widget so better to show it by default.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f9984877eb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.