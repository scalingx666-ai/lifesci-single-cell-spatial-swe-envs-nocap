# Issue

**Title:** fix(windows): stop wsl.exe's stdout becoming the launcher's return value

## Description

Found by a review pass over #58 (already merged). **The Windows package reports "the Linux bundle could not be installed" after installing it successfully — on every machine that actually has WSL2.**

## The defect

In PowerShell a native command's stdout goes to the **success stream**, which is a function's return value. `Invoke-Bootstrap` had:

```powershell
& wsl.exe -d $Distro --exec sh $BootstrapLinux @BootstrapArgs
return $LASTEXITCODE
```

so `return` *appends to* `bootstrap.sh`'s output rather than replacing it. The caller receives `@('installed /home/.../OpenAI4S-...', 0)`, not `0`.

`bootstrap.sh` prints on bare stdout in every **success** path — `already-installed` (`:52`), `installed` (`:87`), `serving http://...` (`:115`) — and sends every failure to stderr. So this fires precisely when the install *worked*:

| step | what happens |
|---|---|
| `$code = Invoke-Bootstrap …` (`:280`) | `$code` is `Object[]`, not `Int32` |
| `if ($code -ne 0)` (`:281`) | array comparison filters to `@(0)`'s complement → one element → non-empty |
| `if` on a non-empty array | **true** |
| `Stop-WithGuidance 'the Linux bundle could not be installed into WSL.'` | exit 1, after a successful install |

The guidance text is itself evidence of the bug: *"The message above says why"* — the message was swallowed into `$code`.

The CLI passthrough breaks harder. `exit $code` at `:267` is handed an `Object[]` and dies on the `Int32` conversion before the passthrough at `:268` ever runs, so `OpenAI4S.cmd status` cannot work at all.

## The fix

`| Out-Host` — one token. It leaves `$LASTEXITCODE` untouched, keeps the return value a plain `Int32`, and puts `bootstrap.sh`'s message back on the console where the guidance already promises the reader it will be. Pure ASCII, so `test_the_windows_launcher_sources_stay_pure_ascii` is unaffected.

## Honest limits of the verification

**This was NOT executed against a real PowerShell** — there is none on this host, and `pwsh` is not installed. The claim rests on documented success-stream semantics plus strong internal corroboration: the launcher itself relies on exactly this behaviour twice on purpose, capturing a native command's stdout with `$x = & native.exe` at `:133` and `:215`.

Repro on any Windows box:

```powershell
function f { & wsl.exe --exec sh -c 'echo installed; exit 0'; return $LASTEXITCODE }
$code = f
$code.Count   # 2, not 1
```

If the analysis is wrong, `| Out-Host` is harmless. If it is right and this ships, the Windows package is broken for its entire intended audience *and* reports "the install failed" after succeeding — the worst possible text for triage.

## Test

`test_the_windows_launcher_does_not_leak_native_stdout_into_its_return_value` asserts every uncaptured `& wsl.exe` call pipes to `Out-Host`. Reverting the one-token change makes it fail. It is a **static** pin on purpose: nothing executes this code — no runner has WSL, so `Invoke-Bootstrap` is unreachable even on the `windows-latest` job, which parses the file and stops at `:121-131`.

`uv run pytest tests/test_release_gates.py` — 31 passed. `uv run pre-commit run --all-files` — every hook passes.

Companion to #67, which fixes the other #58 defect CI structurally cannot reach (the release pipeline's PyPI anchor).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d522c925eb04`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.