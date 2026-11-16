# Issue

**Title:** fix(io): pre-flight the two single-file interleaved paired arms

## Description

`--paired one.bam` and `--paired --output-format ubam one.bam` were the last write-capable dispatch paths with no output-collision pre-flight, and both hand-rolled every output name they wrote. One namer type per arm now produces the writer's paths *and* the pre-flight's candidate list, so the two cannot disagree about what a run writes. Separately, a uBAM write-side read-name refusal now names the read it rejected instead of printing `invalid input parameter` alone. .

Two things worth knowing before merge. No output path changes anywhere — #423 is a pure refactor and #424 adds no reachable refusal, because a collision on those two arms is impossible by construction today; the pre-flight is there for the day something honours `--basename` on them. The only user-visible change is #429's message, and it does not narrow the set of read names Trim Galore accepts.

<details>
<summary>AI-assisted detail</summary>

**Why a struct per arm, not report-only namers.** #423 asked for dedicated namers for the report paths. Done literally, the PR whose first commit deletes two copies of the report strings would have left #424 adding two copies of the *primary* strings — `format!("{}_val_1{}", stem, ext)` and friends. So each arm gets one type covering everything it writes, with `--retain_unpaired` and `--no_report_file` as `Option` fields rather than an `if` repeated at each site.

**What actually makes drift a build error.** `planned()` opens with an exhaustive `let Self { val_1, val_2, unpaired, reports } = self;`. A field added later does not compile until it is enumerated, which is the one mechanism here that earns #423's "unrepresentable" — a `Vec` assembled from `self.foo` accessors does not. This bug family (#383, #388, #391, #398, #409) was always a writer whose path never entered the candidate list, and no type can catch that by describing the candidates that *do* exist.

**Provenance is `OutputSource::Input`, never `Pair`.** These arms have one input, so `Pair` could only be `Pair(x, x)`, which `Display` renders as `one.bam + one.bam`. A unit test drives the refusal message directly to pin that it names a single source.

**Why no test provokes the new refusal.** `file_stem()` strips one `.`-suffix and every appended suffix starts with `_`, so an output can never equal its input; one input means no output-vs-output pair; `guarded_inputs` is a singleton because `--passthrough` needs two inputs and `--demux` is single-end. The tests therefore assert the candidate list's *contents* — over every `Option` combination and `--output_dir` — rather than a refusal.

**The `.gz` row is load-bearing.** `gzip` is `is_gzipped(&cli.input[0])`, which is extension-only, so a `.gz`-*named* BAM produces `.fq.gz` primaries. A candidate list hardcoding `.fq` would pass every other tripwire case here while mis-planning every such run, so there is now a `--paired ip.bam.gz` case; the dump confirms it plans `ip.bam_val_1.fq.gz`.

**The tripwire's three `Arm::Unplanned` cases are promoted, and `fn unplanned` deleted.** It was the variant's only constructor, so leaving it turns `dead_code` into a CI failure under `-D warnings`. The variant and `compare`'s early-return branch stay as the record shape for the next arm that ships without a pre-flight, now driven by their own self-test instead of by three live cases. Both site counts move 11 → 13, with the two shapes added before the count — the order the counter's own failure message asks for.

**Four red tests, not five.** The plan and both plan reviewers predicted that both count assertions would go red at step 5. Only `the_site_inventory_is_complete` does; it reads `main.rs` and counts call sites. `every_site_is_reached_by_some_case` counts distinct sites reached by *its own* hand-listed shapes, so giving an unexercised arm a pre-flight is invisible to it. The two are not redundant — the second is what goes red on a count bumped without a shape added.

**#429's design rested on a wrong assumption, and a probe caught it.** The plan held that a wrapped `TryFromIntError` would not land in `ErrorKind::InvalidInput`, so a kind gate could not cover the 255-byte case. Measured: `@` in a name and a 255-byte name both arrive as `InvalidInput`; 254 bytes is accepted, so the boundary is the SAM limit. One `if` covers both. The gate still earns its place by keeping a full disk or a closed pipe from being relabelled a read-name problem — those get the neutral half alone, which already identifies the record.

**The shown id is capped at 60 characters** with the byte count appended when the cap bites, matching how the aux-tag-framing refusal and the dropped-description notice already show an unbounded value. A FASTQ id has no length limit, and the 255-byte case printed 256 characters on one line before this.

**Verification.** 707 → 722 tests on macOS (720 Linux; the platform-specific four are unchanged). #424's five red-then-green tests were watched go red before step 6 fixed them. #429's message test was proved able to fail by planting the old string back. The `.gz` candidate list, both arms' full candidate lists, and the adversarially-named inputs (`x_val_1.fq`, `y_R1_trimming_report.txt` as BAM inputs — both run to exit 0 with inputs byte-intact) were all measured against the built binary rather than inferred.

**Out of scope, deliberately.** `--gzip` (hidden, Perl-era) is still not consulted by the gzip resolution, which stays extension-only. The `--clump_only` report sites use a different naming scheme and are untouched.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63f5d44830af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.