# Issue

**Title:** build(deps): bump the cargo-patch-minor group with 4 updates

## Description

Bumps the cargo-patch-minor group with 4 updates: [clap](https://github.com/clap-rs/clap), [anyhow](https://github.com/dtolnay/anyhow), [serde_json](https://github.com/serde-rs/json) and [bstr](https://github.com/BurntSushi/bstr).

Updates `clap` from 4.6.1 to 4.6.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/releases">clap's releases</a>.</em></p>
<blockquote>
<h2>v4.6.2</h2>
<h2>[4.6.2] - 2026-07-15</h2>
<h3>Fixes</h3>
<ul>
<li><em>(help)</em> Say <code>alias</code> when there is only one</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/blob/master/CHANGELOG.md">clap's changelog</a>.</em></p>
<blockquote>
<h2>[4.6.2] - 2026-07-15</h2>
<h3>Fixes</h3>
<ul>
<li><em>(help)</em> Say <code>alias</code> when there is only one</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0fe0be3</code></a> chore: Release</li>
<li><a href=""><code>480af9d</code></a> docs: Update changelog</li>
<li><a href=""><code>2b3ddd0</code></a> Merge pull request <a href="">#6340</a> from liskin/fix-completion-escape</li>
<li><a href=""><code>7ffe739</code></a> fix(complete): Do not suggest options after &quot;--&quot;</li>
<li><a href=""><code>d47fc4f</code></a> test(complete): Options suggested after escape (<code>--</code>)</li>
<li>See full diff in <a href="https://github.com/clap-rs/clap/compare/clap_complete-v4.6.1...clap_complete-v4.6.2">compare view</a></li>
</ul>
</details>
<br />

Updates `anyhow` from 1.0.103 to 1.0.104
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dtolnay/anyhow/releases">anyhow's releases</a>.</em></p>
<blockquote>
<h2>1.0.104</h2>
<ul>
<li>Update <code>syn</code> dev-dependency to version 3</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1dbe186</code></a> Release 1.0.104</li>
<li><a href=""><code>f6479f8</code></a> Update to syn 3</li>
<li>See full diff in <a href="https://github.com/dtolnay/anyhow/compare/1.0.103...1.0.104">compare view</a></li>
</ul>
</details>
<br />

Updates `serde_json` from 1.0.150 to 1.0.151
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/serde-rs/json/releases">serde_json's releases</a>.</em></p>
<blockquote>
<h2>v1.0.151</h2>
<ul>
<li>Add RawValue::from_string_unchecked (<a href="">#1331</a>, thanks <a href="https://github.com/WonderLawrence"><code>@​WonderLawrence</code></a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>de85007</code></a> Release 1.0.151</li>
<li><a href=""><code>3b2b3c5</code></a> Merge pull request <a href="">#1331</a> from WonderLawrence/rawvalue-from-string-unchecked</li>
<li><a href=""><code>0406d96</code></a> Debug-assert well-formedness and no-whitespace in from_string_unchecked</li>
<li><a href=""><code>cf16f75</code></a> Add RawValue::from_string_unchecked</li>
<li><a href=""><code>827a315</code></a> Update actions/upload-artifact@v6 -&gt; v7</li>
<li><a href=""><code>cea36a5</code></a> Update actions/checkout@v6 -&gt; v7</li>
<li>See full diff in <a href="https://github.com/serde-rs/json/compare/v1.0.150...v1.0.151">compare view</a></li>
</ul>
</details>
<br />

Updates `bstr` from 1.12.3 to 1.13.0
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>63c6578</code></a> 1.13.0</li>
<li><a href=""><code>9cc49de</code></a> api: add <code>to_bstring()</code>, <code>as_bstring()</code>, and <code>as_bstring_mut()</code> methods to `B...</li>
<li><a href=""><code>7105619</code></a> doc: fix typo &quot;Use <code>&amp;BStr</code> is useful because ...&quot;</li>
<li>See full diff in <a href="https://github.com/BurntSushi/bstr/compare/1.12.3...1.13.0">compare view</a></li>
</ul>
</details>
<br />

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f2418e1501c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.