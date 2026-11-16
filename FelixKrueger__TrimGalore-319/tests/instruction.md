# Issue

**Title:** build(deps): bump the cargo-patch-minor group across 1 directory with 5 updates

## Description

Bumps the cargo-patch-minor group with 5 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [anyhow](https://github.com/dtolnay/anyhow) | `1.0.102` | `1.0.103` |
| [memchr](https://github.com/BurntSushi/memchr) | `2.8.1` | `2.8.2` |
| [log](https://github.com/rust-lang/log) | `0.4.32` | `0.4.33` |
| [env_logger](https://github.com/rust-cli/env_logger) | `0.11.10` | `0.11.11` |
| [bstr](https://github.com/BurntSushi/bstr) | `1.12.1` | `1.12.3` |

Updates `anyhow` from 1.0.102 to 1.0.103
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dtolnay/anyhow/releases">anyhow's releases</a>.</em></p>
<blockquote>
<h2>1.0.103</h2>
<ul>
<li>Fix Stacked Borrows violation (UB) in <code>Error::downcast_mut</code> (<a href="">#451</a>, <a href="">#452</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5bdb0e2</code></a> Release 1.0.103</li>
<li><a href=""><code>e621bd3</code></a> Merge pull request <a href="">#452</a> from dtolnay/downcast</li>
<li><a href=""><code>6e8c000</code></a> Eliminate pointer-&gt;reference-&gt;pointer during downcast</li>
<li><a href=""><code>67c4abd</code></a> Add regression test for issue 451</li>
<li><a href=""><code>917a169</code></a> Update actions/upload-artifact@v6 -&gt; v7</li>
<li><a href=""><code>d9dc3fa</code></a> Update actions/checkout@v6 -&gt; v7</li>
<li><a href=""><code>841522b</code></a> Raise minimum tested compiler to rust 1.85</li>
<li>See full diff in <a href="https://github.com/dtolnay/anyhow/compare/1.0.102...1.0.103">compare view</a></li>
</ul>
</details>
<br />

Updates `memchr` from 2.8.1 to 2.8.2
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a61ac1a</code></a> 2.8.2</li>
<li><a href=""><code>a08bf90</code></a> arch: fix undefined behavior in lower level (but public) APIs</li>
<li><a href=""><code>b41293b</code></a> rebar: update memchr to latest</li>
<li><a href=""><code>87467c9</code></a> impl: remove unnecessary clones in <code>into_owned</code> impls</li>
<li>See full diff in <a href="https://github.com/BurntSushi/memchr/compare/2.8.1...2.8.2">compare view</a></li>
</ul>
</details>
<br />

Updates `log` from 0.4.32 to 0.4.33
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/log/blob/master/CHANGELOG.md">log's changelog</a>.</em></p>
<blockquote>
<h2>[0.4.33] - 2026-06-20</h2>
<h2>What's Changed</h2>
<ul>
<li>Fixed key comparison by <a href="https://github.com/matteo-zeggiotti-ok"><code>@​matteo-zeggiotti-ok</code></a> in <a href="">rust-lang/log#732</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/matteo-zeggiotti-ok"><code>@​matteo-zeggiotti-ok</code></a> made their first contribution in <a href="">rust-lang/log#732</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.32...0.4.33">https://github.com/rust-lang/log/compare/0.4.32...0.4.33</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f405739</code></a> Merge pull request <a href="">#734</a> from rust-lang/cargo/0.4.33</li>
<li><a href=""><code>6a24abf</code></a> prepare for 0.4.33 release</li>
<li><a href=""><code>87e0621</code></a> Merge pull request <a href="">#732</a> from matteo-zeggiotti-ok/fix-key-comparison</li>
<li><a href=""><code>a9b5711</code></a> Review: fallback to the &amp;str hash</li>
<li><a href=""><code>cc89cc6</code></a> Review: fixed other comparisons</li>
<li><a href=""><code>920e7dc</code></a> Review: fixed comparison on <code>MaybeStaticStr</code></li>
<li><a href=""><code>0d71d3c</code></a> Fixed key comparison</li>
<li>See full diff in <a href="https://github.com/rust-lang/log/compare/0.4.32...0.4.33">compare view</a></li>
</ul>
</details>
<br />

Updates `env_logger` from 0.11.10 to 0.11.11
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-cli/env_logger/releases">env_logger's releases</a>.</em></p>
<blockquote>
<h2>v0.11.11</h2>
<h2>[0.11.11] - 2026-06-25</h2>
<h3>Internal</h3>
<ul>
<li>Updated <code>env_filter</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-cli/env_logger/blob/main/CHANGELOG.md">env_logger's changelog</a>.</em></p>
<blockquote>
<h2>[0.11.11] - 2026-06-25</h2>
<h3>Internal</h3>
<ul>
<li>Updated <code>env_filter</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b4d3f2b</code></a> chore: Release</li>
<li><a href=""><code>cc2b2ef</code></a> chore: Release</li>
<li><a href=""><code>69e27d1</code></a> docs: Update changelog</li>
<li><a href=""><code>166880d</code></a> Merge pull request <a href="">#411</a> from epage/parse</li>
<li><a href=""><code>0a580d0</code></a> fix(filter): Remove 'parse' on no_std</li>
<li><a href=""><code>78d8ef1</code></a> Merge pull request <a href="">#404</a> from cagatay-y/feature/filter-no_std</li>
<li><a href=""><code>132fe86</code></a> feat(filter): Add support for no_std environments</li>
<li><a href=""><code>4feafa4</code></a> refactor(env_filter): Fix unreachable pub warning</li>
<li><a href=""><code>92f8d8d</code></a> Merge pull request <a href="">#410</a> from rust-cli/renovate/crate-ci-typos-1.x</li>
<li><a href=""><code>4e57784</code></a> chore(deps): Update pre-commit hook crate-ci/typos to v1.47.0</li>
<li>Additional commits viewable in <a href="https://github.com/rust-cli/env_logger/compare/v0.11.10...v0.11.11">compare view</a></li>
</ul>
</details>
<br />

Updates `bstr` from 1.12.1 to 1.12.3
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cabbfe3</code></a> 1.12.3</li>
<li><a href=""><code>11d6fac</code></a> msrv: decrease to 1.65</li>
<li><a href=""><code>c857a1c</code></a> 1.12.2</li>
<li><a href=""><code>e4c6498</code></a> doc: clarify the case where there is no valid UTF-8 prefix (<a href="">#204</a>)</li>
<li><a href=""><code>8481908</code></a> doc: add alias to <code>fields</code> and <code>Fields</code></li>
<li><a href=""><code>6f089f3</code></a> lint: add <code>set -u</code> to regex generation scripts</li>
<li><a href=""><code>1396d35</code></a> docs: fix spelling mistake</li>
<li><a href=""><code>94cdd94</code></a> lint: add <code>#[must_use]</code> to <code>ByteSlice::replace[n]</code></li>
<li><a href=""><code>155fc93</code></a> deps: switch <code>serde</code> to <code>serde_core</code></li>
<li><a href=""><code>bf0bf16</code></a> perf: implement <code>Iterator::count</code> for <code>Chars</code></li>
<li>Additional commits viewable in <a href="https://github.com/BurntSushi/bstr/compare/1.12.1...1.12.3">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6528e54512e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.