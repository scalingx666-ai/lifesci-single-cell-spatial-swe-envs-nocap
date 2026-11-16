# Issue

**Title:** fix(windows): preserve Unicode paths and bridge Windows Ark CLI

## Description

## Summary

The Windows launcher can corrupt a package path containing Chinese characters under Windows PowerShell 5.1, causing installation or startup to use the wrong WSL path. It also cannot reuse an Ark CLI installed on Windows: the WSL service searches for `arkcli`, while the Windows executable is `arkcli.exe` and its location is not forwarded.

Decode captured WSL output as UTF-8 for the duration of each native invocation, restoring the previous console encoding afterward. Resolve the Windows Ark executable in the launcher, translate its path with `wslpath`, and forward it as one environment argument. An explicitly configured absolute Linux CLI path is also supported. Update the user guide and the README shipped inside the ZIP, and extend the native PowerShell regression coverage.

Targets `main` after the v0.3.0 preparation in #161 was merged. The diff contains four files; it preserves the release's version, frontend, and backend changes.

## Area

- [x] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [x] Test / harness
- [x] Documentation
- [x] Release / packaging

## Verification

Passed:

```text
powershell.exe -NoProfile -NonInteractive -ExecutionPolicy Bypass -File tests/test_windows_launcher.ps1
uv run pre-commit run --all-files
uv run pytest tests/test_release_docs.py tests/test_startup_no_implicit_install.py tests/test_startup_no_implicit_side_effects.py -q
python3 scripts/verify_release_tag.py v0.3.0
git diff --check
```

- Windows PowerShell 5.1: the added native-byte regression fails against the unpatched release launcher and passes against this commit. It also checks stderr/exit-code preservation, restoration of console encoding, CLI discovery, explicit overrides, and argv boundaries for paths with spaces.
- Real Ubuntu 24.04 / WSL2: a Unicode path returned by `wslpath` is corrupted before the patch and preserved afterward. With an installed Windows Ark CLI on the test process's PATH and no Ark-specific `WSLENV` entry, the old launcher forwards no CLI and the WSL lookup exits 127; the patched launcher forwards the translated executable path and its WSL existence check exits 0.
- No account credentials, provider requests, or inference calls are needed by the new regression tests.
- The three release/startup test modules pass (30 tests).
- These local checks passed before rebasing onto the merged main. All four changed files are byte-identical after the rebase.

Not run locally for this commit: the full Python offline suite and the full browser matrix. CI must validate the submitted head; the green release-branch baseline is not claimed as this commit's CI result.

Pending before release: the full v0.3.0 Windows ZIP rebuild and installed-package scientific workflow acceptance. Earlier candidate-package acceptance does not substitute for testing the final v0.3.0 artifact.

## Risk and Reviewer Focus

Review `Invoke-WslCaptureNative`, `Get-WslArkCliPath`, and `Get-WslBootstrapArgs`. Console encoding changes must stay scoped to the native call and restore on failure; CLI paths must stay single argv elements. A CLI must already be installed; the ZIP does not bundle or install Ark CLI. The launcher supports a native Windows `.exe` or an absolute WSL executable path.

## Checklist

- [x] The complete diff is reviewed, small, and focused.
- [x] No unrelated formatting or facade rewrites are included.
- [x] Relevant native tests and real WSL checks are listed above.
- [x] New default tests do not require WSL, credentials, network access, or a model.
- [x] No tests are deleted without replacements.
- [x] No core dependencies are added.
- [x] No secrets, private data, or machine-specific paths are included.
- [x] User-facing documentation matches the launcher behavior.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9563ceb74503`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.