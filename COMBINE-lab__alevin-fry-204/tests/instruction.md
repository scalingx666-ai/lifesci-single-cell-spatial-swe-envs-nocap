# Issue

**Title:** feat(quant): add quant-probe for probe-level quantification

## Description

## Updates before merge (2026-10-24)

Pushed by the maintainers on top of this revision; see the review comment for details.

- **Merged `develop`** (#202, #203, #205-#207). `--dump-molecules` is shared by both subcommands; under `quant-probe` the molecule table projects probe labels onto genes.
- **`-r` in any case.** `quant-probe -r CR-LIKE` panicked. Fixing it exposed an older bug in both subcommands, also in 0.18.3: the `--umi-edit-dist` and `--large-graph-thresh` defaults were matched against `-r` as typed. Both defaults now come from the parsed strategy.
- **`quant-probe -d`** writes `probe_quants_mat_cols.txt`, naming the probe ids in `gene_eqclass.txt.gz`. `infer` now refuses equivalence classes whose ids do not index the `quants_mat_cols.txt` beside them. Before this, it labelled a probe-by-cell matrix with gene names.
- **Probe-set references only.** `quant-probe` counts the reads compatible with two or more targets of one gene. The count is recorded in `quant.json` as `num_same_gene_multimapping_reads`, and a warning fires above 10% of reads. On a transcriptome (PBMC1k) the rate is 48% and `cr-like`/`parsimony` lose about half the UMIs; on a 384-plex Flex v2 library it is 4 of 118M reads.
- **Tests** for ties between probes of one gene (full resolver and fast path, `trivial`, the EM), `featureDump.txt` statistics, `trivial`/`parsimony(-em)` per probe, the same-gene count and warning, upper-case `-r`, and the `infer` refusal. There are 146 tests.
- **Docs and CHANGELOG** state the tie semantics per strategy and the cost.

**Not a breaking change against 0.18.3.** `quant` gives the same output as `develop`, and `quant.json` only gains keys. The "Breaking change" section below concerns only builds of `test/rad-v2-integration`; it ships in 0.19.0 without the `!`.

---

## Since the last review

This revision is stacked on `d01f955` rather than amending it, since that commit is already
merged into `test/rad-v2-integration`. The design question the review opened -- how `quant`
learns that it is looking at probes -- is answered by removing the question: the axis is a
subcommand, so nothing has to be inferred, recorded or read.

## What this does

`alevin-fry quant-probe` quantifies probe-based data -- e.g. 10x Flex. It resolves UMIs per
reference target, so correction, deduplication, tie handling and the EM all act per probe, and
the gene-level count matrix is the sum of each gene's probes. It is the same quantification as
`quant` and takes the same options, minus the ones the probe axis cannot honour and plus
`--probe-mtx`.

`generate-permit-list` no longer records a `data_type` key and `quant` no longer reads one.
`quant` always resolves per gene; `quant-probe` always resolves per reference target. Neither
inspects the data to decide.

`--probe-mtx`, on `quant-probe` only, additionally writes `probe_quants_mat.mtx` -- the
probe-by-cell matrix the gene matrix was summed from -- with its own
`probe_quants_mat_cols.txt` and `probe_quants_mat_rows.txt`. The gene matrix is written either
way, so a probe-level output directory always looks like any other quantification directory,
and the flag adds a matrix rather than selecting between them. It changes what is written, not
what is computed.

## Why a subcommand, and not a data type declared upstream

The review suggested naming every assay and having simpleaf declare it. We went further, because
naming it still leaves alevin-fry acting on a claim it cannot check:

- **Probe-ness is a property of the reference.** Neither the RAD file nor `generate-permit-list`
  sees the reference. A multi-barcode layout says nothing about whether the targets are probes:
  Flex and Parse Bio emit an identical tag-role sequence, and under RAD v2 `known_rad_type` is
  still `TagRole::None`. The self-describing format declines to say "probe", which is the
  strongest argument that the axis is not the file's to declare.
- **Asking the user is exact.** `quant` and `quant-probe` are two entry points into the same
  code. There is no key to get wrong, no older directory that silently means something else, and
  no failure mode where an unreadable JSON file picks an axis.
- **It keeps alevin-fry free of assumptions about the assay.** A reference it has never seen
  quantifies as well as a supported one, and a new probe-based protocol needs no change here.
  Deciding which subcommand an assay calls for belongs one layer up, in the workflow tool that
  resolved the chemistry and built the index -- simpleaf knows both, and can make that choice on
  the user's behalf.

This resolves must-fix 1 (every multi-barcode run treated as Flex) and must-fix 3
(`read_data_type` turning every failure into "not Flex") by deletion: `read_data_type` and
`DATA_TYPE_FLEX` are gone, and the key is written nowhere.

## Must-fix 2: no existing caller is affected

`simpleaf multiplex-quant --usa` and `--resolution parsimony-gene(-em)` keep working exactly as
they do today, because `quant` is unchanged. Measured rather than argued: on the real Flex
library, `quant` from this branch and `develop` produce the same gene matrix, entry for entry
(comparison B below). No simpleaf change is required for this PR to land. Routing Flex to
`quant-probe` -- and refusing `--usa` there, where the reason can actually be explained -- is a
separate simpleaf enhancement.

## Not available under `quant-probe`

Options the probe axis cannot honour are **absent from the subcommand** rather than accepted and
refused at run time, which is also the review's point about `-b` being inconsistent with the
rest:

- `-b, --num-bootstraps`, `--init-uniform`, `--summary-stat` are not defined. The bootstrap
  reports the uncertainty in how the EM allocates a molecule that several features could claim;
  probes are designed to target a single gene with minimal cross-reactivity, so multi-mapping is
  rare enough that the replicates are not informative.
- `--sa-model` is not defined, since it only applies in USA mode.
- `-r` accepts only the strategies that resolve per target. `parsimony-gene` and
  `parsimony-gene-em` build the equivalence map with reads already projected to genes, so the UMI
  graph is deduplicated per gene and no per-probe assignment survives to sum; they are refused by
  name, pointing at `parsimony` / `parsimony-em`.
- A three-column (USA) transcript-to-gene map is an error. Two separate reasons, worth stating
  because simpleaf already generates `probe_t2g_usa.tsv` for any probe CSV with a `region`
  column, so the mislabelling risk predates this PR (simpleaf will stop generating that file;
  index directories already written still carry it, which is why this refusal earns its place):
  1. A probe set's status column does not mean what USA mode's does. 10x marks a probe `spliced`
     when it spans an exon-exon junction and `unspliced` when it does not -- in which case it
     cannot tell mature from nascent transcript. A non-junction probe is therefore *ambiguous* in
     USA terms, not unspliced, and a transcriptome probe set carries no nascent-specific probe.
     Read as a splicing state, the column would put 46,022 of the 53,519 included probes of the
     human v2 set into the unspliced layer, while those probes mostly measure mature mRNA. 10x
     uses the two classes of one gene to estimate genomic-DNA background, which is what the
     column is for.
  2. The state USA mode reports is a resolution outcome, not an annotation: a UMI reaches a
     gene's ambiguous slot by being compatible with both of its variants, which relies on the
     overlapping transcripts of a transcriptome reference. A probe reference carries little such
     overlap.
- An input directory produced in velocity mode, which has its own feature axis and no probe axis
  to sum.

With `--dump-eqclasses` the ids in `gene_eqclass.txt.gz` are probe ids and its first line is the
number of probes. The file format is positional, so it cannot carry that caveat itself; the run
warns instead and the file is not renamed.

## Breaking change (relative to `test/rad-v2-integration` only)

Nothing breaks against any release: 0.18.3 never switched axes. Against the
`test/rad-v2-integration` build, `quant` on a probe-based collated RAD now quantifies on the
gene axis instead of switching to the probe axis. Probe-based data is quantified by asking for `quant-probe`.

This reaches anyone following the RAD v2 test-build document, which pins
`test/rad-v2-integration`: on that commit `quant` switches axes on Flex, and after this revision
it does not. Worth deciding whether to re-pin that document before re-merging.

## For crate users

`QuantOpts` gains `probe_level: bool` (default `false`) beside `probe_mtx: bool`. `quant.json`
records `feature_axis` (`"probe"` or `"gene"`) in place of `data_type`, and keeps `probe_mtx`,
`num_probes` and `probe_nnz`. `generate_permit_list.json` loses `data_type`.

## Measured on real data

The review asked for the Flex gene matrix compared with `develop`, which the PR's own validation
did not cover. Same columns as the kidney table, our library.

> **10x Flex v2, 16k Human PBMC TotalSeq-C, 4-plex.** Chromium Human Transcriptome Probe Set
> v2.0.0 (GRCh38-2024-A): 53,519 included probes over 18,132 genes, so the resolver's axis is
> 2.95x wider than the gene axis. 403,299 barcodes, ~144.6M UMIs. `develop` (`edfd1aa`) and this
> PR quantified the **same** collation (14.9 GB `map.collated.rad`), 16 threads, back to back in
> one job on an uncontended node, page cache warmed first; wall time and peak RSS are the median
> of 3 repeats, counts come from repeat 1. The host is an EPYC-7402, so read the wall-time column
> as the relative change rather than comparing its absolute seconds with the kidney numbers.

### The four resolution strategies, each at its default `--umi-edit-dist`

`cr-like` and `cr-like-em` default to 0, the parsimony family to 1.

| resolution | gene entries differing (of ~49M) | net change in total | wall time, develop -> PR | peak RSS, develop -> PR |
|---|---|---|---|---|
| cr-like | 20,292 (0.041%; 17,691 lower / 2,601 higher) | -16,497 UMIs (-0.011%) | 15.2 -> 15.6 s (+3%) | 1.34 -> 1.40 GB |
| cr-like-em | 367,743 (0.749%; 192,864 lower / 174,879 higher) | ~0 (-205 UMIs) | 15.6 -> 16.2 s (+4%) | 1.36 -> 1.40 GB |
| parsimony | 105 (0.000%; 105 lower / 0 higher, each +/-1 or less) | ~0 (-105 UMIs) | 17.4 -> 17.9 s (+2%) | 1.45 -> 1.44 GB |
| parsimony-em | 164 (0.000%; 142 lower / 22 higher, each +/-1 or less) | ~0 (-102 UMIs) | 17.5 -> 18.2 s (+4%) | 1.47 -> 1.48 GB |

### `cr-like --umi-edit-dist 1`, the configuration we recommend for Flex

Cell Ranger-style Hamming-1 UMI collapsing, which is what the Flex work on this library uses and
what the paper reports. It is also the worst case for the probe axis: enabling the correction
forces the tiny-cell fast path off, so every one of the 403,299 cells goes through the full
resolver rather than the ~384k of them that the fast path would otherwise take.

| resolution | gene entries differing (of ~49M) | net change in total | wall time, develop -> PR | peak RSS, develop -> PR |
|---|---|---|---|---|
| cr-like | 42,670 (0.087%; 20,836 lower / 21,834 higher) | +16,518 UMIs (+0.012%) | 16.6 -> 18.0 s (+9%) | 1.50 -> 1.55 GB |

Reading of it:

- At each strategy's default the change is small and in the expected direction. The probe axis
  refuses to resolve a UMI whose reads hit two probes of one gene, which the gene axis counts:
  `cr-like` loses 16,497 of ~144.6M UMIs, 0.011%.
- `cr-like-em` moves many more *entries* (0.75%) but almost no *mass* (-205 UMIs net). The EM
  spreads an ambiguous UMI instead of discarding it, and since the two probes belong to the same
  gene the gene total comes back whole.
- `parsimony` and `parsimony-em` barely move at all (about 100 entries, each by 1): they build
  the UMI graph at transcript level and project only after covering it, so they were already
  resolving per target.
- **`--umi-edit-dist 1` reverses the sign**, which is worth stating rather than burying. The
  Hamming-1 collapse acts *within a feature*, so on the probe axis two near-identical UMIs on two
  probes of one gene no longer merge into one molecule. Fewer collapses means more molecules
  counted, and it outweighs the ambiguity loss: `cr-like` goes from -16,497 UMIs at ed0 to
  +16,518 at ed1, with a roughly even lower/higher split rather than only losses.
- Our per-entry rates are higher than the kidney library's -- about 33x for `cr-like` -- which is
  worth saying plainly: the effect is small, but it is not negligible, and it is
  library-dependent.

One caveat on the "differing" column. `cr-like` and `parsimony` are integer counts, so any
difference there is real. The `-em` strategies accumulate in f32 in HashMap iteration order, so a
rerun of the *same* binary already moves the last bits and the column is an upper bound rather
than a measurement: above the 1e-5 relative tolerance our validation gates use, `cr-like-em`
differs in 356,109 entries (0.725%) rather than 367,743, and the other three are unchanged.

## Cost of the wider axis

The resolver now runs over every reference target rather than every gene -- 53,519 probes against
18,132 genes, 2.95x. For every cell outside the tiny-cell fast path, `em_optimize` allocates two
dense vectors over all features, `unique_evidence` / `no_ambiguity` are cleared over all
features, and a dense `counts` vector is scanned. These patterns are on `develop` already; the
probe axis multiplies their cost.

Measured in the table above, at each strategy's default `--umi-edit-dist`: `cr-like` +3%,
`cr-like-em` +4%, `parsimony` +2%, `parsimony-em` +4%, with peak RSS within a few percent
throughout. The worst case in the grid is `cr-like --umi-edit-dist 1`, 16.6 -> 18.0 s (+9%),
where enabling the Hamming-1 UMI correction forces the tiny-cell fast path off and all 403,299
cells go through the full resolver instead of the ~384k that would otherwise take the fast path.

The sparse EM would remove most of this. `em_optimize_subset_with_scratch` (`src/em.rs:279`)
works on the sparse equivalence-class subset instead of a dense per-feature vector, but it is
reached only from the `usa_mode == true` arms of `quant.rs`; the non-USA arms call the dense
`em_optimize`. Extending it to the probe axis is left as a follow-up **because it changes the
non-USA EM path for every dataset, not only probe-based data** -- it wants its own PR and its own
numeric validation rather than riding along here.

## Design notes

- **`pugutils.rs` is untouched.** At probe level the resolver is handed an identity map
  (`[0, 1, ..., ref_count-1]`), so its existing projection step projects each target to itself and
  the equivalence classes come out probe-keyed. The real `tid_to_gid` is demoted to an
  output-stage projection table. One `FeatureAxis`, built in one place, carries both.
- **`em.rs` is untouched**, and so is every bootstrap path in `quant.rs`.
- **The summation is one insertion point.** Every branch -- tiny-cell fast path, small, large,
  trivial, EM, parsimony -- converges on the same sparse `expressed_ind` / `expressed_vec`, which
  is summed into genes there. It is a sparse accumulator cleared as it is read, plus a sort over
  only the genes touched, so it costs O(entries) per cell.
- **Per-cell statistics are taken after the summation**, on the gene axis, with or without
  `--probe-mtx`, so `featureDump.txt` has the same columns and the same values either way and
  `NumGenesExpressed` / `NumGenesOverMean` keep counting genes. `sum_umi` is invariant under the
  sum; `max_umi` and `num_expr` are not, so they are recomputed.
- **The two matrices are row-aligned by construction**: a cell's row index is taken once from the
  shared counter, under the same lock that appends that cell's barcode, and both matrices are
  pushed at that index. The row labels are nevertheless written a second time under the probe
  matrix's own name, so a reader can load either matrix from its own triple of files. (Row
  *order* differs between runs, since the RAD reader is parallel; it never differs between the
  two matrices of one run.)

## Validation

| | compared | result |
|---|---|---|
| **A** | this branch `quant-probe` vs `d01f955`'s probe axis | every statistic of C reproduces `d01f955`'s exactly |
| **B** | this branch `quant` vs `develop` `edfd1aa`'s gene axis | **0 differing entries**, in all five configurations |
| **C** | this branch `quant-probe` vs `develop` `edfd1aa` | the grid table above |

**B** is the hard form of the must-fix 2 claim: `quant` from this branch and from `develop`
produce the same gene matrix on the real Flex library, entry for entry, with identical nonzero
counts and identical totals, under `cr-like` and `cr-like-em` at both `--umi-edit-dist` settings
and under `parsimony` and `parsimony-em`. No existing caller, simpleaf included, can be affected
by this PR.

**A** is not a direct matrix diff -- the `d01f955` binary was rebuilt over -- but every number in
C reproduces what `d01f955` produced against the same `develop` build: 20,292 entries,
17,691 lower / 2,601 higher, -16,497 UMIs for `cr-like`, and likewise for the other three
strategies. The revision changed how the axis is selected and nothing that is computed on it.

Tests: 113 passed at this revision (146 after the updates at the top). The ones this PR adds cover reads hitting two probes of one gene and two probes
of different genes, under `cr-like` (both with the tiny-cell fast path on and off) and
`cr-like-em`, i.e. the cases where the two axes genuinely differ -- the synthetic fixture in the
previous revision had one probe per read, so "gene matrix = probe matrix summed by gene" held
trivially. The three refusals (`-b`, a 3-column tg-map, `parsimony-gene(-em)`) are covered too,
including that a 3-column map on the gene axis is still ordinary USA-mode quantification.

## Review items, mapped

| review item | where |
|---|---|
| must-fix 1, multi-barcode treated as Flex | removed; the axis is the subcommand |
| must-fix 2, simpleaf options would start failing | `quant` is byte-identical to `develop` (B) |
| must-fix 3, `read_data_type` swallows errors | `read_data_type` deleted |
| suggestion, name every assay | superseded; nothing is recorded or read |
| efficiency, note the dense per-feature cost | "Cost of the wider axis" above |
| repeated `probe_level_out` accessor | `probe_writer` |
| duplicated matrix finalisation and column writer | `finish_matrix`, `write_label_file` |
| five scattered `if probe_level` branches | one `FeatureAxis` |
| `num_genes` / `num_rows` now hold probe counts | renamed `num_features` / `feature_rows` |
| `hdr.ref_names.clone()` | borrowed |
| `-b` warned while others errored | all refusals are errors |
| no test where the axes differ | added |
| `write_tg_map` near-copies | share one helper |

## Revision history

**2026-10-23.** This description was rewritten for the `quant-probe` design. The original
description -- of the inferred `data_type` design that the review above discusses -- is in this
body's edit history, and the commits that implemented it are still in the branch. Nothing in the
review was dismissed: the two behaviour problems and the error-handling gap are answered by
removing the inference rather than refining it, and the duplication, clarity and test items are
addressed in place. See the table at the end of the previous section for where each one landed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ad78c1bb630`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.