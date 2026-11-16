# Issue

**Title:** feat(gpl): add opt-in frequency-weighted cell barcode correction

## Description

## What this changes

This PR adds an optional frequency-weighted correction strategy for cell barcodes used with `generate-permit-list --unfiltered-pl`:

```text
--cell-bc-correction <unique|frequency>
```

`unique` remains the default and preserves alevin-fry's historical, conservative rule: an unmatched barcode is corrected only when it has exactly one retained single-substitution neighbour. `frequency` resolves multiple retained neighbours by their Laplace-smoothed pre-correction read counts and accepts the best candidate only when it has at least 97.5% of the total candidate weight.

The name deliberately describes what the implementation can establish from a RAD file. This is Cell Ranger-inspired, but it is not an exact Cell Ranger reproduction:

- RAD stores packed barcodes without base qualities. With uniform qualities, Cell Ranger's common error-probability factor cancels and the rule reduces to the frequency prior used here.
- Cell Ranger considers the full whitelist. alevin-fry considers only barcodes retained after `--min-reads`, preserving the existing meaning of its unfiltered permit-list workflow.

The strategy applies to both ordinary RNA and per-sample multiplex RNA permit-list generation. It does not affect filtered RNA correction, sample-barcode correction, or ATAC.

## Audit repairs

The maintainer follow-up makes several correctness and quality changes:

- freezes all candidate weights before correcting any unmatched barcode, matching Cell Ranger's documented requirement that counts are observed **prior to correction** and preventing order-dependent cascading priors;
- replaces an allocated `3 * barcode_length` neighbour vector and repeated concurrent-map lookups with allocation-free substitution enumeration and an indexed weight vector;
- represents the 0.975 threshold exactly as the integer ratio 39/40;
- applies the strategy to multiplex/per-sample cell barcodes and records it in both single- and multi-barcode run metadata;
- keeps strategy-neutral logging and adds focused tests for the historical default, absent/unique/ambiguous candidates, the exact threshold, aligned weights, frozen priors, and stable serialized names;
- removes an unrelated per-thread dense EM scratch change that was included in the original commit. Sparse EM remains exactly as implemented on current `master`.

## Independent real-data evaluation

On the PBMC RAD from the alevin-fry 0.17 parity manifest (`-t 8`, pinned to eight physical cores):

| Strategy | Corrected reads | Ambiguous reads | Permit-map entries |
| --- | ---: | ---: | ---: |
| `unique` (default) | 983,308 | 62,254 | 149,885 |
| `frequency` | 1,043,664 | 1,898 | 152,024 |

The optional strategy rescues 60,356 additional reads. The default map is semantically identical to the existing reference, and the repaired frequency map is semantically identical to the submitted implementation on this dataset. Seven repeated repaired runs produced identical deserialized maps.

Seven warmed, interleaved repetitions:

| Variant | Whole GPL median (range / MAD) | Correction phase median | Peak RSS median |
| --- | ---: | ---: | ---: |
| original `unique` | 1.700 s (1.700–1.720 / 0.000) | 71.125 ms | 331,408 KiB |
| original `posterior` | 1.800 s (1.780–2.230 / 0.010) | 154.116 ms | 332,532 KiB |
| repaired `unique` | 1.700 s (1.690–1.700 / 0.000) | 71.470 ms | 338,528 KiB |
| repaired `frequency` | 1.730 s (1.730–1.740 / 0.000) | 105.784 ms | 333,048 KiB |

The optimized frequency correction phase is 31.4% faster than the submitted implementation. Whole-stage overhead versus the default is about 1.8%, and measured peak memory does not increase.

The Flex fixture also completed under both strategies. All 28 non-empty per-sample maps matched the historical path on this small fixture, and metadata records `"cell_bc_correction": "frequency"`.

## Validation

- `cargo fmt --all -- --check`
- `cargo clippy --workspace --all-targets --all-features -- -D warnings`
- `cargo test --workspace`: 34 passed, 1 intentionally ignored real-data test
- release build and dependency feature-tree inspection
- CLI dependency check: `frequency` requires `--unfiltered-pl`

Current fixup commit: `1978eca` (after merging current `master` at `7c7a99d`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c7a99d61520`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.