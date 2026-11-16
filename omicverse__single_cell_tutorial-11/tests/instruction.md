# Issue

**Title:** Add repository hex sticker

## Description

## Summary

Adds the repository hex sticker for `single_cell_tutorial`.

## Files

- `logo/logo.svg`
- `logo/logo.png`

## Notes

This sticker is a visual identifier for the repository in the omicverse ecosystem. It does not replace the official omicverse brand logo.

## Checks

- SVG and 1600x1600 PNG included.
- No SVG `<text>` or font-family dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94a874febdf4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.