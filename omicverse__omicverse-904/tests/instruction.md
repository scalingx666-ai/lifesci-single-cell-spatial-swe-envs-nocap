# Issue

**Title:** feat(alignment): homology search (DIAMOND/BLAST+) + Sanger .ab1 verification

## Description

Two additions to `ov.alignment`, both verified against real data with the real binaries.

## 1. `homology_search` / `reciprocal_best_hits` — free the DIAMOND path

The fast homology path already existed but was **trapped**: SAMap's `build_blast_maps` drove DIAMOND with auto-detect and a concurrent two-direction run (~100-1000× faster than `blastp`), yet nothing outside `external/samap` could reach it, and it carried no `@register_function` — so an agent could not discover it either.

```python
ov.alignment.homology_search(query, subject, method=...)
#   'auto'     -> DIAMOND if installed, else blastp (protein-protein)
#   'diamond' | 'diamond-blastp' | 'diamond-blastx'
#   'blastp' | 'blastx' | 'blastn' | 'tblastn' | 'tblastx'   (NCBI BLAST+)
ov.alignment.reciprocal_best_hits(a, b)   # RBH ortholog pairs
```

Both engines emit outfmt-6 with identical columns, so one tidy DataFrame contract covers both. Failures surface the aligner's stderr instead of an empty `CalledProcessError`. `external/samap/_run.py` now **delegates** instead of keeping a private copy; its `maps/` output is unchanged.

Docstrings point at `single.get_orthologs` for species with curated Ensembl orthology — a precomputed one-to-one lookup beats re-deriving it, and RBH is for what lookup cannot serve (unannotated assemblies, distant species, designed sequences).

**Bug found while verifying with real data:** the search DB was built beside `out` under a fixed name, so two concurrent searches writing into one directory — exactly what a reciprocal run does — clobbered each other's database and one direction silently searched the **wrong subject** (mouse-vs-mouse at 100% identity). The DB now always lives in a private temp dir; a regression test pins it.

Verified with human/mouse GAPDH + TP53 against **DIAMOND 2.2.4** and **BLAST+ 2.17.0**: both engines call the same pairs at 93.7% / 77.3% identity, and RBH recovers both.

## 2. Sanger `.ab1` — the construct-verification loop

Nothing in omicverse could read a chromatogram (a grep for `sanger|ab1|chromatogram` found only a CSS colour). This closes a loop the package already opens: `ov.synbio` designs a construct and writes its GenBank; this checks the sequencing that came back against it.

```python
ov.alignment.read_ab1(path)          # SangerTrace: primary+secondary basecall,
                                     #   per-base quality, four dye channels
ov.alignment.basecall(path, ...)
ov.alignment.align_to_reference(...)
ov.alignment.decompose_trace(...)    # alleles from a MIXED trace
ov.alignment.verify_construct(...)   # pass/fail + exact mismatches
```

Engine is **tracy** (EMBL, BSD) — the only well-maintained open implementation of mixed-trace decomposition, which is how a heterozygous variant or a CRISPR-edited allele is read off one overlapping chromatogram. `read_ab1` also has a pure-Biopython path so a trace loads without tracy. GenBank references are accepted and converted internally.

**Design correction found by running real data, not by reading docs:** judging a clone on whole-read identity *fails correct constructs*. A real trace against its own basecall — a perfect clone by construction — scored **0.9571 with 50 differences**, and all 50 were in the last 50 bases and were **gaps, zero substitutions**: ordinary Sanger end decay. `align_to_reference` now also reports `identity_core` / `core_differences` (alignment minus `edge_margin` per end) and `verify_construct` decides on that. The same trace now passes at core identity **1.0000**, while a planted substitution is still located at exactly the right position.

The docstring states the threshold caveat plainly: one substitution in a ~1 kb read is still ~0.999 identity and clears the default, so a construct you intend to *use* should require `core_differences == []`, not just `ok`.

## Placement

Both live in `ov.alignment` rather than a new namespace: it already owns external sequence binaries via `resolve_executable`/`auto_install` (mafft, fastp, STAR, cutadapt), and neither of these transforms an AnnData — which is what `ov.tl` documents itself as. `_INSTALL_HINTS` gains diamond / the BLAST programs / tracy.

## Tests

**33 pass** — command construction, method resolution and parsing run anywhere; 9 end-to-end tests use the real binaries and **skip cleanly (reported, never silently passed)** when they are absent.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Follow-up in this branch: `read_ab1(engine='auto')` was silently degrading

`auto` resolved tracy with `shutil.which`, which only looks at `PATH`, while every other function in the module used `resolve_executable`, which *also* checks the interpreter's own `env/bin`. A tracy installed into the active environment (the normal case under a managed kernel) was therefore invisible to `auto` alone, and it fell through to the Biopython parser — **no secondary basecall, no dye channels, and no warning that the trace had been read the lesser way**. A 1165 bp trace came back reporting "0 channels".

`auto` now resolves with the same rule as the rest of the module. Re-measured on the same file: 4 channels, 16302 samples, 11 mixed positions.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43bc8ac66e3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.