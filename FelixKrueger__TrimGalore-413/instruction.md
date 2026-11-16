# Issue

**Title:** feat(io): collision refusals name the inputs behind each output

## Description

The pre-flight hashed prospective output paths without recording which input each was named from, so its advice could not be followed. A report collision printed the same path twice —

```
out/reads.fq_trimming_report.txt and out/reads.fq_trimming_report.txt would be
written to the same file … rename one input
```

— and then told the user to rename an input it could not name. Now:

```
the outputs named from a/reads.fq and b/reads.fq would be written to the same
file, out/reads.fq_trimming_report.txt
```

`preflight_output_collisions` takes `&[(PathBuf, OutputSource)]`, where `OutputSource` is `Input(p)` or `Pair(a, b)`. Four message shapes: output-vs-input names the input the offending output derives from; two sources sharing one rendered path name both and print the path once; differing spellings (fold-equal, or `./x` vs `x`) show both paths with their sources; and **one input feeding two candidates gets its own advice**.

That last shape is the new behaviour and the reason it was in scope: `trim_galore --paired A.fq B.fq B.fq C.fq` is permitted by validation (only *exact* duplicate pairs are rejected) and was refused with advice nobody could act on, since a file cannot be renamed apart from itself. It now says to list each input once.

Which runs are accepted or refused is unchanged. Every pinned substring is preserved — `PREFIX`, `DUP_MSG`, `ALIAS_MSG`, and the CI-grepped `case-insensitive, for APFS/NTFS safety` — so no existing assertion or `ci.yml` grep changes. 570 tests green.

<details>
<summary>AI-assisted: the design decisions, and an honest limit on what the type buys</summary>

Scope was 11 call sites, 4 helper signatures, 13 test call expressions — mapped by a planning pass, then re-derived from the compiler rather than trusted, since two merges had shifted the plan's line numbers.

**Paired primaries use a uniform `Pair` source** rather than the more pointed `Input(r1)` for `_val_1`. `Input(r1)` is exact today, but it encodes a claim about which mate supplies the directory — precisely what #398 may change. Uniform `Pair` keeps this landable before #398 is decided. The clump paired-BAM per-pair report keeps `Input(chunk[0])` despite its siblings saying `Pair`, because R1 genuinely is the source there and renaming R2 would not resolve the collision; truthful beats symmetric.

**What the type does not buy.** It makes an *unattributed* candidate impossible, but it cannot detect a *missing* one — which is what #383, #385, #388, #391 and #409 all were. The durable fix for that family is one derivation feeding both the candidate list and the writers, or #391's exact-set assertion extended across all 11 arms. Recorded in the function's own doc comment so the next reader isn't misled about the guarantee.

One test needed re-scoping rather than fixing: `preflight_appends_hint_only_when_given` began failing because my test helper derived each source from its path, so two identical paths produced the *same* source and correctly landed in the one-input shape — which ignores the hint by design. Re-scoped to the two-source shape, with a separate test pinning the hint-suppression. Had I "fixed" it by making that shape carry the hint, I'd have reintroduced the unfollowable advice.
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0bb76b52a73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.