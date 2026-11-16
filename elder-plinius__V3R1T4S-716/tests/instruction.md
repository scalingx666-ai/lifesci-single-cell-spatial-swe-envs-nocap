# Issue

**Title:** kit: preserve spaces in configured bank paths

## Description

With `bank: custom bank/target list.json` in `settings.md`, `load_bank()` tries only `custom` before falling back to another bank. A valid target from the configured bank can consequently be rejected as unknown, and malformed JSON at the intended path is never read or reported. The same truncation affects absolute paths containing spaces.

Use the full value already parsed by `kv()`, which removes Markdown wrapping. Keep the existing absolute/relative path resolution and fallback order. Add six regressions covering relative and absolute paths, an existing first-word filename, workspace target selection, and malformed-bank diagnostics through both workspace and package checks. Clarify path formatting in `kit/SETUP.md`.

Validation:

- All six new tests fail against the original implementation.
- `python3 -m unittest discover -s kit/tests -p 'test_*.py' -v`: all 90 tests pass on Linux with Python 3.11.15 and 3.14.4.
- Trial merges with #629 and #636 are clean. The combined snapshot passes all 93 tests on both Python versions with Windows text-newline translation emulated. Native Windows has not been run.
- Python 3.8 syntax parsing and `git diff --check` pass.

The release-wide `SHA256SUMS` is left for regeneration against the final merged tree.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ebdef41c304`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.