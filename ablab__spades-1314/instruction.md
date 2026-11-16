# Issue

**Title:** Fix for package managers storing files in read-only

## Description

This is a quick fix coming from a hack I had to do for the packaging of Spades 4.0.0 into NixOS : 

- https://nixos.org/
- https://github.com/NixOS/nixpkgs/tree/master/pkgs/by-name/sp/spades

The proposed patch is currently into the proposed update for the Nix Spades package, but it would be great if the fix is done upstream. The problem is that once installed, a Nix package has all the files with no write permission at all (files coming from packages are stored into a read-only directory). The Spades pipeline copies some data files to an output directory, but keeps the modes, even if the `preserve_mode` argument is set to `false` because it uses the `shutil.copytree()` function that implies a `shutil.copystat()` that can not be disabled (see https://github.com/python/cpython/blob/4bf17c381fb7b465f0f26aecb94a6c54cf9be2d3/Doc/library/shutil.rst?plain=1#L237). So the copied files are read-only and the test pipeline fails. 
Giving the write access to the owner is enough to solve the issue.

Co-authored by: Andrey Prjibelski <andrewprzh@gmail.com>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60ad35e88074`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.