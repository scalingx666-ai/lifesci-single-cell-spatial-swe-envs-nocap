# Issue

**Title:** chore(release): v2.2.0 (Clumpify Edition)

## Description

## Summary

Cuts v2.2.0 — the Clumpify Edition. This PR is the version-bump-and-CHANGELOG commit that gates the release.yml dispatch on master.

\`\`\`diff
- version = \"2.1.0\"
+ version = \"2.2.0\"
\`\`\`

### Scope of v2.2.0 vs v2.1.0 GA

| Area | Source |
|---|---|
| Phil Ewels' \`--clumpify\` / \`--compression\` / \`--memory\` feature trio | #282 |
| WGBS-vs-RRBS perf-data drops backing the per-data-type guidance | #283 |
| \`--high_compression\` flag **removed** (subsumed by \`--compression <N>\`) | #282 |
| Workflow model: dev = canonical truth, master = release pin | #284 → #285 |
| When-to-use bullet list updated: RRBS in low-complexity yes-list, WGBS framing softened to \"may have detrimental impact\" | #286 |
| Integer-arithmetic max_errors in adapter alignment (#262 Item A) | #287 |
| Memory & I/O reference data folded into Threading model docs (#263 + #264) | #287 |

### Release plan after this merges

1. **FF master to dev** — \`git push origin origin/dev:master\`
2. **Trigger \`release.yml\` on master** via workflow_dispatch
3. release.yml fires the GA path on master + version-string \`2.2.0\` → publishes binaries (Linux x86_64/aarch64 + macOS arm64), GHCR \`:latest\` / \`:v2.2.0\` / \`:v2.2\` / \`:v2\`, crates.io publish, GitHub Release with the v2.2.0 tag
4. Bioconda recipe bump (separate PR on bioconda-recipes — \`2.1.0\` → \`2.2.0\` + 3 new sha256s)
5. Optional Discussion #215 announcement

## Test plan

- [x] \`cargo build --release\` clean — version banner reads \`trim_galore 2.2.0 (Oxidized Edition)\`
- [x] \`npm run build\` (docs) clean
- [ ] CI green on this PR (Lint, Rust Tests ubuntu+macos, Coverage, Reproducibility, Validate-vs-Perl, Security audit)
- [ ] After merge to dev + FF master to dev: trigger release.yml; all 12 jobs green
- [ ] Post-release: \`cargo install trim-galore\` resolves to 2.2.0; \`docker pull ghcr.io/felixkrueger/trimgalore:latest\` resolves to v2.2.0 multi-arch image

Closes the v2.2.0 release milestone.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea62d67d7cfc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.