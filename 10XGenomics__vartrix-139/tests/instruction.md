# Issue

**Title:** Bump csv from 1.2.2 to 1.4.0

## Description

Bumps [csv](https://github.com/BurntSushi/rust-csv) from 1.2.2 to 1.4.0.
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4a3997e</code></a> 1.4.0</li>
<li><a href=""><code>a0a3c9e</code></a> csv-core-0.1.13</li>
<li><a href=""><code>f8e6b07</code></a> deps: switch <code>serde</code> dependency to <code>serde_core</code></li>
<li><a href=""><code>7c7c135</code></a> style: address many Clippy lints</li>
<li><a href=""><code>5b2da18</code></a> doc: simplify tutorial section on accessing headers</li>
<li><a href=""><code>633552a</code></a> perf: serialize 128-bit integers via <code>itoa</code></li>
<li><a href=""><code>e9f06f4</code></a> lint: fix <code>needless_lifetimes</code> and <code>mismatched_lifetime_syntaxes</code></li>
<li><a href=""><code>9dab947</code></a> test: fix broken test after panic message change</li>
<li><a href=""><code>da00088</code></a> style: address many Clippy lints</li>
<li><a href=""><code>f973cd4</code></a> enum: use <code>#[non_exhaustive]</code> instead of <code>#[doc(hidden)]</code> variant</li>
<li>Additional commits viewable in <a href="https://github.com/BurntSushi/rust-csv/compare/1.2.2...1.4.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=csv&package-manager=cargo&previous-version=1.2.2&new-version=1.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d959b7e659cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.