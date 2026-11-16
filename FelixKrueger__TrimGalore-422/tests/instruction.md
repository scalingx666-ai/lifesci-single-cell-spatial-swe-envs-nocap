# Issue

**Title:** test(io): empirical exact-set tripwire over the output-collision pre-flight

## Description

The output-collision pre-flight has shipped the same defect five times (#383, #388, #391, #409, and the report hole #398 closed) — always a writer whose path never entered the candidate list, so the pre-flight silently stopped covering that output. This adds a tripwire that makes it un-shippable: the pre-flight can now dump the candidate list it is about to check, and a new test snapshots the tree per dispatch arm, runs it, and asserts every file the run created was in that list. No behaviour changes and no candidate-assembly code is touched, so candidate order — which decides which path a collision message names — is untouched. Test hook is inert unless `TRIM_GALORE_DUMP_PLANNED_OUTPUTS` is set. 589 → 643 tests.

Addresses #414.

<details>
<summary>AI-assisted detail</summary>

**Why a hook rather than a unit test.** The candidate lists are assembled in `main.rs`, a `[[bin]]`, so nothing in `tests/` can reach them. Every past fix therefore compared writer output against a hand-written expectation, which is why each of the five instances needed a human to notice the omission first — the problem is observability, not diligence. `preflight_output_collisions` gains `#[track_caller]` and prints its candidate list plus the calling site when the env var is set; all 11 call sites funnel through it, so one place exposes every arm.

**What it asserts.** T1: every created file was in the dumped list (only this direction — over-planning is legitimate, since `--retain_unpaired` plans `_unpaired_N` whether or not anything strands). T3: no pre-existing file's bytes changed, which is #409's harm asserted directly. T4: the run created something and a planned arm dumped something — clap's `DisplayHelpOnMissingArgumentOrSubcommand` exits 0 to stdout, so a case with a quoting slip would otherwise satisfy every subset relation vacuously. T5: no run reaches two distinct pre-flight sites. Comparison uses the production `io::collision_key`, so the test shares the pre-flight's own case-folded notion of "same path".

**Coverage.** 41 arm cases over all 15 dispatch arms and 11 sites, including the two single-file interleaved paired arms that have no pre-flight at all — those assert T3 plus "nothing was dumped", so the day either gains one, the case goes red and says to promote it. 12 self-tests prove each assertion can fail, and `the_site_inventory_is_complete` pins the site count so a 12th arm cannot appear without touching the suite.

Expectations are derived by observation throughout; hand-enumerating them would relocate the original knowledge problem into a test file. `--fastqc` output is the one known-unplanned write set, allowed by rule rather than by list and scoped to the arms that can actually reach `fastqc::run` (#421) — an allowance that can go red on a legitimate case is the strongest argument for deleting it.

**Verified by mutation, not inspection.** Adding a writer with no candidate turns the relevant cases red naming the unplanned paths, the site, and the full candidate list. Both reviewers ran that independently, and one reviewer's mutation was live in the shared tree while another agent was running — so two agents independently watched the tripwire catch a writer neither had planted.

Green under `cargo test`, `cargo test --release` and `cargo nextest run`; clippy `-D warnings` and rustfmt clean. No `cfg` gate on the hook: CI runs both the debug nextest and the release `cargo test`, so a `debug_assertions` gate would silently no-op the tripwire in the release run.

**Deliberately not here.** Per-case arm identity stays documented rather than asserted (all 21 shapes hand-verified to route correctly today). The structural single-derivation fix still needs candidate order normalised first. Dedicated paired report namers are a follow-up, since they edit the very code this tripwire polices and should land under it.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3008b37ff366`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.