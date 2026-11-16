# Issue

**Title:** Plot method, and new figure

## Description

Add plotting method for SlideData and Tile objects. It's pretty basic, only works with RGB images and OpenSlideBackend for now (BioFormatsBackend thumbnail extraction was hanging for me). But better to have barebones implementation than nothing.

Also added updated overview figure to docs and README

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d04fc56e6cec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.