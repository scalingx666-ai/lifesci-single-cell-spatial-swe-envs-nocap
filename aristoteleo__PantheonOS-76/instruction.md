# Issue

**Title:** Add WSL browser fallback for auto-ui

## Description

## Summary

This PR improves `pantheon ui --auto-start-nats --auto-ui` when running inside WSL.

## Changes

- detect WSL environments before opening the auto-connect URL
- prefer launching the Windows default browser via `powershell.exe` / `cmd.exe` fallback
- keep the existing `webbrowser.open(...)` behavior for non-WSL environments
- add tests covering WSL detection and Windows browser fallback behavior
- document the WSL behavior in the UI quickstart docs

## Motivation

On WSL, `webbrowser.open(...)` may fall back to Linux browser handlers such as `xdg-open`, which can fail when no Linux desktop browser is installed. In that case, `--auto-ui` generates the correct connection URL but does not open the Pantheon UI automatically.

This change makes `--auto-ui` work more reliably for WSL users by opening the URL with the Windows default browser instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfd3f159edbc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.