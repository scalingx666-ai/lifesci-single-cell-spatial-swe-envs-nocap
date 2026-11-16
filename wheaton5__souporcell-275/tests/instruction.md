# Issue

**Title:** Bump rand from 0.7.2 to 0.9.3 in /souporcell

## Description

Bumps [rand](https://github.com/rust-random/rand) from 0.7.2 to 0.9.3.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-random/rand/blob/0.9.3/CHANGELOG.md">rand's changelog</a>.</em></p>
<blockquote>
<h2>[0.9.3] — 2026-02-11</h2>
<p>This release back-ports a fix from v0.10. See also <a href="">#1763</a>.</p>
<h3>Changes</h3>
<ul>
<li>Deprecate feature <code>log</code> (<a href="">#1764</a>)</li>
<li>Replace usages of <code>doc_auto_cfg</code> (<a href="">#1764</a>)</li>
</ul>
<p><a href="">#1763</a>: <a href="">rust-random/rand#1763</a></p>
<h2>[0.9.2] — 2025-07-20</h2>
<h3>Deprecated</h3>
<ul>
<li>Deprecate <code>rand::rngs::mock</code> module and <code>StepRng</code> generator (<a href="">#1634</a>)</li>
</ul>
<h3>Additions</h3>
<ul>
<li>Enable <code>WeightedIndex&lt;usize&gt;</code> (de)serialization (<a href="">#1646</a>)</li>
</ul>
<h2>[0.9.1] - 2025-04-17</h2>
<h3>Security and unsafe</h3>
<ul>
<li>Revise &quot;not a crypto library&quot; policy again (<a href="">#1565</a>)</li>
<li>Remove <code>zerocopy</code> dependency from <code>rand</code> (<a href="">#1579</a>)</li>
</ul>
<h3>Fixes</h3>
<ul>
<li>Fix feature <code>simd_support</code> for recent nightly rust (<a href="">#1586</a>)</li>
</ul>
<h3>Changes</h3>
<ul>
<li>Allow <code>fn rand::seq::index::sample_weighted</code> and <code>fn IndexedRandom::choose_multiple_weighted</code> to return fewer than <code>amount</code> results (<a href="">#1623</a>), reverting an undocumented change (<a href="">#1382</a>) to the previous release.</li>
</ul>
<h3>Additions</h3>
<ul>
<li>Add <code>rand::distr::Alphabetic</code> distribution. (<a href="">#1587</a>)</li>
<li>Re-export <code>rand_core</code> (<a href="">#1604</a>)</li>
</ul>
<h2>[0.9.0] - 2025-01-27</h2>
<h3>Security and unsafe</h3>
<ul>
<li>Policy: &quot;rand is not a crypto library&quot; (<a href="">#1514</a>)</li>
<li>Remove fork-protection from <code>ReseedingRng</code> and <code>ThreadRng</code>. Instead, it is recommended to call <code>ThreadRng::reseed</code> on fork. (<a href="">#1379</a>)</li>
<li>Use <code>zerocopy</code> to replace some <code>unsafe</code> code (<a href="">#1349</a>, <a href="">#1393</a>, <a href="">#1446</a>, <a href="">#1502</a>)</li>
</ul>
<h3>Dependencies</h3>
<ul>
<li>Bump the MSRV to 1.63.0 (<a href="">#1207</a>, <a href="">#1246</a>, <a href="">#1269</a>, <a href="">#1341</a>, <a href="">#1416</a>, <a href="">#1536</a>); note that 1.60.0 may work for dependents when using <code>--ignore-rust-version</code></li>
<li>Update to <code>rand_core</code> v0.9.0 (<a href="">#1558</a>)</li>
</ul>
<h3>Features</h3>
<ul>
<li>Support <code>std</code> feature without <code>getrandom</code> or <code>rand_chacha</code> (<a href="">#1354</a>)</li>
<li>Enable feature <code>small_rng</code> by default (<a href="">#1455</a>)</li>
<li>Remove implicit feature <code>rand_chacha</code>; use <code>std_rng</code> instead. (<a href="">#1473</a>)</li>
<li>Rename feature <code>serde1</code> to <code>serde</code> (<a href="">#1477</a>)</li>
<li>Rename feature <code>getrandom</code> to <code>os_rng</code> (<a href="">#1537</a>)</li>
<li>Add feature <code>thread_rng</code> (<a href="">#1547</a>)</li>
</ul>
<h3>API changes: rand_core traits</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1aeee9f</code></a> Prepare v0.9.3: deprecate feature <code>log</code> (<a href="">#1764</a>)</li>
<li><a href=""><code>98473ee</code></a> Prepare rand 0.9.2 (<a href="">#1648</a>)</li>
<li><a href=""><code>031a1f5</code></a> <code>examples/print-next.rs</code> (<a href="">#1647</a>)</li>
<li><a href=""><code>6cb75ee</code></a> Make UniformUsize serializable (<a href="">#1646</a>)</li>
<li><a href=""><code>0c955c5</code></a> Add some tests for BlockRng, BlockRng64 and Xoshiro RNGs (<a href="">#1639</a>)</li>
<li><a href=""><code>204084a</code></a> Fix: Remove accidental editor swap file (<a href="">#1636</a>)</li>
<li><a href=""><code>86262ac</code></a> Deprecate rand::rngs::mock module and StepRng (<a href="">#1634</a>)</li>
<li><a href=""><code>a6e217f</code></a> Update statrs link (<a href="">#1630</a>)</li>
<li><a href=""><code>db993ec</code></a> Prepare rand v0.9.1 (<a href="">#1629</a>)</li>
<li><a href=""><code>3057641</code></a> Remove zerocopy from rand (<a href="">#1579</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/rust-random/rand/compare/0.7.2...0.9.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rand&package-manager=cargo&previous-version=0.7.2&new-version=0.9.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/wheaton5/souporcell/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `398abcc4bee2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.