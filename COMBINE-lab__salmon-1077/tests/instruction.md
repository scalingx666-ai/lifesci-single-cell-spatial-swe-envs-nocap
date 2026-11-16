# Issue

**Title:** fix(genemap): report and remedy a gene map that matches no quantified transcript

## Description

.

Unmatched transcripts stay dropped rather than reverting to C++'s transcript-as-its-own-gene fallback, and both migration documents now say so instead of claiming parity. Rationale in "A correction to the code" below; say the word if you want the fallback restored and I will send it as its own change.

## The problem

An index built from the Ensembl cDNA FASTA quantifies `ENST00000622028.1`. The Ensembl GTF says `transcript_id "ENST00000622028"` and puts the version in a separate `transcript_version` attribute. `write_gene_quant` joins them with a literal string compare, so the match rate is not low, it is **zero** — and `quant.genes.sf` comes out with only its header, exit code 0.

## salmon was not silent — it was contradictory

I assumed "no warning" when I filed #1075 and that was wrong; the code disproved it. `main.rs:878` does warn. The problem is the line after it. Running unpatched `develop` against a 15-transcript index whose FASTA is versioned and whose GTF is not:

```
warning: 15 transcript(s) had no entry in the gene map and were omitted from quant.genes.sf
wrote gene-level estimates for 15 genes to quant.genes.sf
```

```
$ wc -l out/quant.genes.sf
       1
```

"wrote gene-level estimates for 15 genes" — to a file with **zero** gene rows. `n_genes` was counted from the gene map, not from what was written:

```rust
let n_genes = map.values().collect::<HashSet<_>>().len();
println!("wrote gene-level estimates for {n_genes} genes to quant.genes.sf");
```

So the run's last word is a success message, on stdout, contradicting a warning on stderr. That is the actual defect: not silence, but a reassuring summary that is wrong.

## After

Same input, same branch, no flag — behaviour unchanged, diagnosis added:

```
warning: 15 of 15 transcript(s) had no entry in the gene map and were omitted from quant.genes.sf
warning: the gene map matched only 0 of 15 quantified transcripts (0.0%); quant.genes.sf has 0 gene row(s)
warning: 15 would match with --ignoreTxVersion, which compares identifiers without their
         trailing version suffix (e.g. NM_001168316.1 vs NM_018953). The Ensembl cDNA FASTA
         carries transcript versions in the identifier while the GTF puts them in a separate
         transcript_version attribute, so an index built from the FASTA does not join to the
         GTF as-is.
wrote gene-level estimates for 0 genes to quant.genes.sf
```

The third warning only fires when ignoring versions would genuinely match more, so it diagnoses rather than guesses. With the flag:

```
$ salmon quant … -g annotation.gtf --ignoreTxVersion
wrote gene-level estimates for 15 genes to quant.genes.sf

$ wc -l out/quant.genes.sf
      16
```

Mass is conserved through the join:

| | TPM | NumReads |
|---|---|---|
| `quant.sf` | 1000000.000 | 10000.000 |
| `quant.genes.sf` | 1000000.000 | 10000.000 |

And the flag is inert when identifiers already agree — same index, a GTF whose `transcript_id` carries the version, with and without `--ignoreTxVersion`:

```
--- identical output with and without the flag? ---
IDENTICAL
```

## Summary of changes

| | |
|---|---|
| `write_gene_quant` return | `usize` → `GeneQuantSummary { matched, unmapped, genes_written }` |
| CLI summary line | counts gene-map genes → counts rows written |
| low match rate | undetected → warns at ≤ `LOW_MATCH_RATE` (0.5) |
| cause | unstated → names the version mismatch when that is demonstrably it |
| remedy | none → `--ignoreTxVersion`, off by default |

**On the threshold.** 0.5, justified in the doc comment where it is defined. The failure mode is total — a version mismatch matches nothing — and a correctly paired annotation matches essentially everything, so the two regimes are far apart and the exact cut is not delicate. Half means the majority of what was quantified is missing from the output, which is worth flagging in any workflow, while a deliberately partial annotation (single-chromosome GTF, spike-in-only map) is nowhere near being mistaken for correct. It gates a warning only; nothing fails, nothing changes.

**On the default.** `--ignoreTxVersion` is off deliberately, and I would push back on making it automatic. The complaint in #1075 is that a bad join produced an empty file without saying so; stripping versions implicitly would replace a silent wrong answer with a silent right one and leave the next mismatch just as invisible. Version-aware annotations are also a legitimate setup. Semantics match tximport's flag of the same name, so the name should already mean the right thing to users. `strip_tx_version` only strips when the final dot-separated part is all digits, so GENCODE's `ENST00000456328.2_PAR_Y` survives.

## A correction to the code

The doc comment on `write_gene_quant` said unmatched transcripts are skipped "(salmon's behavior)". That is not what C++ salmon did — `aggregateEstimatesToGeneLevel` emitted each unmatched transcript as its own single-transcript gene and warned once per transcript:

```cpp
auto gn = tgm.geneName(er.target, foundGene);   // returns transcriptName when not found
if (!foundGene) { logger->warn("… returning transcript as it's own gene", er.target); }
geneExps[gn].push_back(std::move(er));          // emitted regardless
```

So on this input C++ 1.x wrote 515,982 rows and half a million warnings — useless as gene-level output, impossible to miss. 2.x drops them and reported success.

This branch keeps the dropping and documents it, rather than restoring the C++ fallback. Emitting every unmatched transcript as its own gene turns a failed join into a `quant.genes.sf` full of transcript IDs posing as genes — 515,982 plausible-looking rows that a downstream `tximport` or `DESeq2` will happily consume — which is harder to notice than an empty file, not easier. What C++ had going for it was the half-million warnings, and the warnings added in commit 2 carry that signal without the junk output. The doc comment now records the reasoning.

`MIGRATION.md` and `migrating/from-cpp.mdx` listed `-g/--geneMap` under *Unchanged*; commit 5 moves it to *Behavior differences to be aware of* in both, and lists `--ignoreTxVersion` under *New in 2.0*.

## Commits

1. `test(genemap): cover a gene map that matches no quantified transcript` — characterisation test; asserts the *current* outcome, passes as-is, so the following commits move against a documented baseline.
2. `fix(genemap): warn when the gene map matches few or no transcripts` — no change to matching.
3. `feat(genemap): add --ignoreTxVersion to strip trailing version suffixes` — opt-in.
4. `docs: document --ignoreTxVersion and the Ensembl cDNA + GTF pitfall`
5. `docs: correct the C++ parity claim for -g/--geneMap`

Verified per commit, not just at the tip — `cargo fmt --all --check`, `cargo clippy -p salmon-core -p salmon-cli --all-targets`, `cargo test`:

```
14a56b7e test(genemap): cover a gene map that matches no q | fmt=OK clippy_err=0 test_fail=0
bf185c84 fix(genemap): warn when the gene map matches few  | fmt=OK clippy_err=0 test_fail=0
01074258 feat(genemap): add --ignoreTxVersion to strip tra | fmt=OK clippy_err=0 test_fail=0
2d7d6a4d docs: document --ignoreTxVersion and the Ensemb | fmt=OK clippy_err=0 test_fail=0
79fb7cd1 docs: correct the C++ parity claim for -g/--gen | fmt=OK clippy_err=0 test_fail=0
```

`cargo test --workspace` is green at the tip. salmon-core goes from 20 to 27 tests.

## Note on the API and the plumbing

`write_gene_quant` now returns a struct and takes an `ignore_tx_version` flag — a breaking change to a `pub fn` in salmon-core, with salmon-cli the only caller in-tree. The gene-map path and the flag travel together as a small `GeneMapOpts` rather than as a bare `bool` threaded through `run_deterministic` and the other two quantification entry points; that keeps their arity unchanged and keeps the option attached to the path it qualifies. Happy to do it the other way if you prefer.

## Deliberately not addressed

- **Other identifier mismatches** (GENCODE `|`-delimited FASTA headers, RefSeq/Ensembl crossovers). The low-match-rate warning will now flag them, but only the version case gets a named cause and a flag, because it is the one with a settled convention to copy from tximport.
- **The gzip issue (#1074)** is independent and is #1076; no overlap with this branch beyond both touching `genemap.rs`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6925149381b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.