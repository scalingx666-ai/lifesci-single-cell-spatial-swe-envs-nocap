# Issue

**Title:** deps: declare paraseq-temp under its real name

## Description

Follow-up to the finding on #1170: the manifest renamed this dependency, and the rename made it invisible to Dependabot.

## The rename was never load-bearing

```toml
paraseq = { package = "paraseq-temp", version = "0.5.0-pre.2" }
```

`paraseq-temp`'s own manifest declares `[lib] name = "paraseq"`, so `use paraseq::...` resolves identically with or without the rename key. Not one line of code changes in this PR, and `Cargo.lock` is untouched: same crate, same version.

The comment above the entry says the rename exists so that `use paraseq::...` is unchanged. That reason does not hold, and the hazard the comment warns about (two paraseq copies either side of piscem-rs's API) is unrelated to the key: piscem-rs resolves `paraseq-temp` too, which is visible in `Cargo.lock`, and that is what keeps the two sides on one crate.

## What it cost

Dependabot's cargo parser drops a renamed manifest entry before building a dependency from it:

```ruby
# cargo/lib/dependabot/cargo/file_parser.rb, manifest_dependencies
next unless name == name_from_declaration(name, requirement)
```

`name` is `paraseq`, `name_from_declaration` returns `paraseq-temp`, so the entry is skipped. The crate then reaches the parser only through `Cargo.lock`, with no requirement attached, which makes it indirect and puts it outside the default `allow`.

Measured by running that parser over this workspace in the official updater image, before and after:

```
before   paraseq-temp   0.5.0-pre.2   TRANSITIVE (no manifest requirement)
after    paraseq-temp   0.5.0-pre.2   direct (1 req)
```

Everything else is unchanged in both runs (374 dependencies parsed either way; piscem-rs, libradicl, cf1-rs, sshash-lib, ksw2rs all direct as before).

## Why it matters beyond Dependabot

This is a pinned pre-release of a republished crate, waiting on noamteyssier/paraseq#78 to land upstream. It is exactly the dependency whose movement someone should be told about, and it was the one dependency no tool could see. The comment now records why it is not renamed, so the next person who finds `paraseq-temp = ...` uglier than `paraseq = ...` does not quietly undo it.

With this in, the `paraseq-temp` pattern in #1170's `combine-lab-upstream` group starts matching, which is the state that PR's description assumed. I will update its inline note once one of the two lands; whichever order suits you.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adbbaee6abe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.