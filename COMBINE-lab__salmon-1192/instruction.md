# Issue

**Title:** chore(deps): bump the cargo-patch group across 1 directory with 3 updates

## Description

Bumps the cargo-patch group with 3 updates in the / directory: [thiserror](https://github.com/dtolnay/thiserror), [statrs](https://github.com/statrs-dev/statrs) and [clap](https://github.com/clap-rs/clap).

Updates `thiserror` from 2.0.19 to 2.0.20
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dtolnay/thiserror/releases">thiserror's releases</a>.</em></p>
<blockquote>
<h2>2.0.20</h2>
<ul>
<li>Suppress redundant_field_names clippy lint in generated code (<a href="">#454</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b1d5db5</code></a> Release 2.0.20</li>
<li><a href=""><code>c4c3ebd</code></a> Merge pull request <a href="">#454</a> from dtolnay/clippy</li>
<li><a href=""><code>2266152</code></a> Suppress redundant_field_names clippy lint</li>
<li><a href=""><code>2901cfd</code></a> Raise minimum tested compiler to rust 1.88</li>
<li><a href=""><code>aa9d91f</code></a> Update ui tests for version 2.0.19</li>
<li>See full diff in <a href="https://github.com/dtolnay/thiserror/compare/2.0.19...2.0.20">compare view</a></li>
</ul>
</details>
<br />

Updates `statrs` from 0.19.0 to 0.19.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/statrs-dev/statrs/releases">statrs's releases</a>.</em></p>
<blockquote>
<h2>v0.19.1</h2>
<h3>Added</h3>
<ul>
<li>let callers choose the binomial sampling algorithm</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Correct exact distribution boundaries</li>
<li>Beta::sf returning exactly 1.0 for tiny x</li>
<li>order the selection fast paths by total_cmp, not &lt;=</li>
<li>replace hand-rolled quickselect with select_nth_unstable_by</li>
<li>address review on the BINV/BTPE sampler</li>
</ul>
<h3>Other</h3>
<ul>
<li>Alias f64 constants</li>
<li>Fix nightly f64 deprecation warnings</li>
<li>add a selection benchmark, and ordered fast paths it exposed</li>
<li>build the NaN order-statistic test under no_std</li>
<li>move binomial sampling into its own module</li>
<li>split the sampler's branch selection out of the RNG path</li>
<li>require std for the BTPE chi-square test</li>
<li>sample Binomial via BINV/BTPE instead of n Bernoulli trials</li>
<li>Bound the Newton iteration count and cover the quantile guards</li>
<li>Add safeguarded-Newton inverse_cdf for Chi and InverseGamma</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/statrs-dev/statrs/blob/main/CHANGELOG.md">statrs's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/statrs-dev/statrs/compare/v0.19.0...v0.19.1">0.19.1</a> - 2026-08-11</h2>
<h3>Added</h3>
<ul>
<li>let callers choose the binomial sampling algorithm</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Correct exact distribution boundaries</li>
<li>Beta::sf returning exactly 1.0 for tiny x</li>
<li>order the selection fast paths by total_cmp, not &lt;=</li>
<li>replace hand-rolled quickselect with select_nth_unstable_by</li>
<li>address review on the BINV/BTPE sampler</li>
</ul>
<h3>Other</h3>
<ul>
<li>Alias f64 constants</li>
<li>Fix nightly f64 deprecation warnings</li>
<li>add a selection benchmark, and ordered fast paths it exposed</li>
<li>build the NaN order-statistic test under no_std</li>
<li>move binomial sampling into its own module</li>
<li>split the sampler's branch selection out of the RNG path</li>
<li>require std for the BTPE chi-square test</li>
<li>sample Binomial via BINV/BTPE instead of n Bernoulli trials</li>
<li>Bound the Newton iteration count and cover the quantile guards</li>
<li>Add safeguarded-Newton inverse_cdf for Chi and InverseGamma</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4775e87</code></a> chore: update MSRV lockfile</li>
<li><a href=""><code>8b8a4ee</code></a> chore: release v0.19.1</li>
<li><a href=""><code>a73c016</code></a> chore: Alias f64 constants</li>
<li><a href=""><code>a77efb3</code></a> chore: Fix nightly f64 deprecation warnings</li>
<li><a href=""><code>f1a7c52</code></a> fix: Correct exact distribution boundaries</li>
<li><a href=""><code>0901747</code></a> fix: Beta::sf returning exactly 1.0 for tiny x</li>
<li><a href=""><code>02fdab6</code></a> fix: order the selection fast paths by total_cmp, not &lt;=</li>
<li><a href=""><code>91f128b</code></a> perf: add a selection benchmark, and ordered fast paths it exposed</li>
<li><a href=""><code>86af064</code></a> test: build the NaN order-statistic test under no_std</li>
<li><a href=""><code>c66c7c7</code></a> fix: replace hand-rolled quickselect with select_nth_unstable_by</li>
<li>Additional commits viewable in <a href="https://github.com/statrs-dev/statrs/compare/v0.19.0...v0.19.1">compare view</a></li>
</ul>
</details>
<br />

Updates `clap` from 4.6.4 to 4.6.6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/releases">clap's releases</a>.</em></p>
<blockquote>
<h2>v4.6.6</h2>
<h2>[4.6.6] - 2026-08-06</h2>
<h3>Features</h3>
<ul>
<li>Add <code>Command::get_overridden_usage</code></li>
</ul>
<h2>v4.6.5</h2>
<h2>[4.6.5] - 2026-07-31</h2>
<h3>Fixes</h3>
<ul>
<li><em>(help)</em> Correctly mark which <code>value_names</code> are optional with <code>num_args</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/blob/master/CHANGELOG.md">clap's changelog</a>.</em></p>
<blockquote>
<h2>[4.6.6] - 2026-08-06</h2>
<h3>Features</h3>
<ul>
<li>Add <code>Command::get_overridden_usage</code></li>
</ul>
<h2>[4.6.5] - 2026-07-31</h2>
<h3>Fixes</h3>
<ul>
<li><em>(help)</em> Correctly mark which <code>value_names</code> are optional with <code>num_args</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>348cff3</code></a> chore: Release</li>
<li><a href=""><code>d478377</code></a> docs: Update changelog</li>
<li><a href=""><code>04b9fbb</code></a> Merge pull request <a href="">#6414</a> from koopatroopa787/fix-bash-completion-bracket-glob</li>
<li><a href=""><code>7075239</code></a> Merge pull request <a href="">#6422</a> from BaumiCoder/fix-fish-indentations</li>
<li><a href=""><code>f90a966</code></a> fix(complete): Use spaces for indentation in fish</li>
<li><a href=""><code>dd4997b</code></a> fix(complete): Don't glob-expand bash positionals</li>
<li><a href=""><code>8387c81</code></a> Merge pull request <a href="">#6399</a> from clap-rs/renovate/crate-ci-typos-1.x</li>
<li><a href=""><code>8141e11</code></a> chore(deps): Update compatible (dev) (<a href="">#6398</a>)</li>
<li><a href=""><code>8a6bd4e</code></a> chore(deps): Update pre-commit hook crate-ci/typos to v1.47.0</li>
<li><a href=""><code>71a7213</code></a> chore(deps): Update Rust Stable to v1.96 (<a href="">#6396</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/clap-rs/clap/compare/clap_complete-v4.6.4...clap_complete-v4.6.6">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e5ccb29caa7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.