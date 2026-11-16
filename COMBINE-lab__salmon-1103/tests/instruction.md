# Issue

**Title:** feat(io): detect input compression from content, shared across input paths

## Description

Fixes the non-FASTQ half of #1102.

### The problem

salmon decided "is this compressed, and how" independently at four entry points, with four different answers:

| path | mechanism | accepted |
| --- | --- | --- |
| `salmon index -t` | `needletail`, sniffs content | gzip, bzip2, xz, zstd |
| `--geneMap` | `niffler`, sniffs magic bytes | gzip, bzip2, xz, zstd |
| `quant -a -t` | hand-rolled 2-byte gzip magic check | gzip only |
| `quant -1/-2` | file-extension match on `.gz` | `.gz`-named gzip only |

So `salmon index -t transcripts.fa.zst` worked while `quant -a -t transcripts.fa.zst` did not, and a perfectly ordinary gzip file that was not named `.gz` was rejected with

```
Invalid start character (), expected either '>' or '@'
```

which describes the decompressed format that never happened, rather than the compression that was not detected.

### The change

Adds `salmon_core::compress`, a single helper over `niffler` — already a workspace dependency and already used by `--geneMap` — and routes the transcriptome FASTA (`load_ref_bytes`) and the SAM reader through it. Detection is by magic bytes, so a correctly compressed file is read whatever it is called, and gzip goes through `MultiGzDecoder` so multi-member and BGZF files are read in full rather than truncated at the first member.

`genemap` keeps its path-annotated error messages but now delegates the decoding, so there is one implementation rather than two that happen to agree.

`is_sam_path` still decides SAM-vs-BAM by extension. That is a different question from how the bytes are compressed, and it stays as it was.

### The FASTQ path is deliberately excluded

I had it implemented and dropped it: per your answer on #1102, `open_reader` will be replaced by piscem 0.9's decoder selection with auto-balanced mapping/decompression threads. No point landing something that is about to be replaced.

One thing worth checking when 0.9 lands, phrased as a question rather than a request: is its decoder selection format-general, or gzip-centric? If the latter, `-1/-2` would still reject zstd/bz2/xz while every other salmon input accepts them, and the helper added here is the piece that would compose with it. Entirely your call — I am not proposing anything for that path now.

### Verification

`quant -a -t`, all four forms of the same transcriptome, at `-p 1`:

| form | result |
| --- | --- |
| `t.fa` | ✅ |
| `t.fa.gz` | ✅ byte-identical `quant.sf` |
| gzip named `t.fa.gzip` | ✅ byte-identical |
| `t.fa.zst` | ✅ byte-identical |

and byte-identical to develop's own plain `-p 1` run, so the decoding change alters nothing else.

`--geneMap` still accepts plain / gz / zstd after being rewired onto the shared helper. The reads path is confirmed unchanged (zstd still rejected there, as intended).

Comparisons are at `-p 1` deliberately: alignment mode is not run-to-run reproducible at `-p > 1` (#1098), so a multi-threaded comparison here would measure that rather than this change.

Three unit tests on the helper cover content-sniffing regardless of file name, multi-member gzip being read to the end, and a file too short to sniff opening as plain text. Full suite green, clippy clean, fmt clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6b6b28a5990`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.