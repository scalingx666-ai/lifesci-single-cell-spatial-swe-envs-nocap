# Issue

**Title:** Bump human-panic from 1.1.5 to 2.0.4

## Description

[//]: # (dependabot-start)
⚠️  **Dependabot is rebasing this PR** ⚠️

Rebasing might not happen immediately, so don't worry if this takes some time.

Note: if you make any changes to this PR yourself, they will take precedence over the rebase.

---

[//]: # (dependabot-end)

Bumps [human-panic](https://github.com/rust-cli/human-panic) from 1.1.5 to 2.0.4.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-cli/human-panic/blob/main/CHANGELOG.md">human-panic's changelog</a>.</em></p>
<blockquote>
<h2>[2.0.4] - 2025-10-28</h2>
<h2>[2.0.3] - 2025-07-08</h2>
<h3>Internal</h3>
<ul>
<li>Update toml</li>
</ul>
<h2>[2.0.2] - 2024-10-10</h2>
<h3>Fixes</h3>
<ul>
<li>Improve detection of what can be trimmed from backtrace</li>
</ul>
<h2>[2.0.1] - 2024-07-25</h2>
<h3>Compatibility</h3>
<ul>
<li>Update MSV to 1.74</li>
</ul>
<h2>[2.0.0] - 2024-04-17</h2>
<h3>Compatibility</h3>
<ul>
<li>Update MSV to 1.73</li>
<li><code>PanicStyle</code> is now non-exhaustive</li>
<li><code>Method</code> is now non-exhaustive</li>
<li><code>Metadata</code>s fields are now private, requiring setters</li>
</ul>
<h3>Features</h3>
<ul>
<li>Add <code>Metadata::support</code> for where to send reports</li>
</ul>
<h2>[1.2.3] - 2024-01-12</h2>
<h3>Internal</h3>
<ul>
<li>Update anstream</li>
</ul>
<h2>[1.2.2] - 2023-11-06</h2>
<h3>Performance</h3>
<ul>
<li>Improve build times by only pullin in <code>toml</code> rendering, not parsing</li>
</ul>
<h2>[1.2.1] - 2023-09-28</h2>
<h3>Internal</h3>
<ul>
<li>Update anstream</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b8915ed</code></a> chore: Release</li>
<li><a href=""><code>1fdc7e3</code></a> Merge pull request <a href="">#183</a> from epage/docs</li>
<li><a href=""><code>7c81b00</code></a> fix: Remove stale nightly implementation</li>
<li><a href=""><code>55acb2b</code></a> docs: Don't enable nightly feature for docs.rs</li>
<li><a href=""><code>e9ec8a0</code></a> Merge pull request <a href="">#181</a> from rust-cli/renovate/actions-setup-python-6.x</li>
<li><a href=""><code>6bd12af</code></a> chore(deps): Update actions/setup-python action to v6</li>
<li><a href=""><code>0b35c87</code></a> Merge pull request <a href="">#180</a> from rust-cli/renovate/actions-checkout-5.x</li>
<li><a href=""><code>ae2aeaa</code></a> style: Fix spelling</li>
<li><a href=""><code>6bed154</code></a> chore(deps): Update actions/checkout action to v5</li>
<li><a href=""><code>c6e394a</code></a> Merge pull request <a href="">#179</a> from epage/template</li>
<li>Additional commits viewable in <a href="https://github.com/rust-cli/human-panic/compare/v1.1.5...v2.0.4">compare view</a></li>
</ul>
</details>
<br />

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b6db0153b69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.