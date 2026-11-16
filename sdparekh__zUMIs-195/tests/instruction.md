# Issue

**Title:** Create shadow YAML file for correcting errors, warn about changes

## Description

This patch creates an intermediate YAML file, `<name>.corrected.yaml`, which is used as the working file for YAML changes, so that the input file can remain unchanged. Where a change is necessary, a warning is emitted.

I have also made additional style consistency / security changes:

* Remove excess whitespace from line endings
* Make indentation consistent
* Make for / if loop layouts consistent (e.g. placing ` ; then` on the line before the first execution step)
* Add braces to guard variables (useful when file names and YAML options contain unexpected characters)
* Change backticks to `$()` [nestable and increases file name protection; useful for at least `zumisdir` variable setting]

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcac30f46e98`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.