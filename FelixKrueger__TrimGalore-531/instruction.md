# Issue

**Title:** build(deps): bump the cargo-patch-minor group across 1 directory with 5 updates

## Description

Bumps the cargo-patch-minor group with 5 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [clap](https://github.com/clap-rs/clap) | `4.6.6` | `4.6.7` |
| [flate2](https://github.com/rust-lang/flate2-rs) | `1.1.9` | `1.1.10` |
| [gzp](https://github.com/sstadick/gzp) | `2.0.3` | `2.0.4` |
| [log](https://github.com/rust-lang/log) | `0.4.33` | `0.4.35` |
| [serde_json](https://github.com/serde-rs/json) | `1.0.151` | `1.0.154` |

Updates `clap` from 4.6.6 to 4.6.7
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/releases">clap's releases</a>.</em></p>
<blockquote>
<h2>v4.6.7</h2>
<h2>[4.6.7] - 2026-09-14</h2>
<h3>Features</h3>
<ul>
<li><em>(derive)</em> Add <code>#[command(defer = &lt;bool&gt;)]</code> attribute to opt-in to lazy initialisation of subcommands</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/blob/main/CHANGELOG.md">clap's changelog</a>.</em></p>
<blockquote>
<h2>[4.6.7] - 2026-09-14</h2>
<h3>Features</h3>
<ul>
<li><em>(derive)</em> Add <code>#[command(defer = &lt;bool&gt;)]</code> attribute to opt-in to lazy initialisation of subcommands</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d3e59a9</code></a> chore: Release</li>
<li><a href=""><code>d997f87</code></a> docs: Update changelog</li>
<li><a href=""><code>fb6058c</code></a> Merge pull request <a href="">#6409</a> from heaths/pwsh-support</li>
<li><a href=""><code>2310870</code></a> test(complete): Add tests for completer_for_path</li>
<li><a href=""><code>5967c17</code></a> refactor(complete): Move shell detection to Shells</li>
<li><a href=""><code>594602b</code></a> fix(complete): Detect pwsh for PowerShell</li>
<li><a href=""><code>3a4f2d0</code></a> Merge pull request <a href="">#6427</a> from clap-rs/renovate/shlex-2.x</li>
<li><a href=""><code>67ebaed</code></a> Merge pull request <a href="">#6426</a> from clap-rs/renovate/actions-checkout-7.x</li>
<li><a href=""><code>c968b13</code></a> chore(deps): Update Rust crate shlex to v2</li>
<li><a href=""><code>8f247cb</code></a> chore(deps): Update actions/checkout action to v7</li>
<li>Additional commits viewable in <a href="https://github.com/clap-rs/clap/compare/clap_complete-v4.6.6...clap_complete-v4.6.7">compare view</a></li>
</ul>
</details>
<br />

Updates `flate2` from 1.1.9 to 1.1.10
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/flate2-rs/releases">flate2's releases</a>.</em></p>
<blockquote>
<h2>1.1.10</h2>
<h2>What's Changed</h2>
<ul>
<li>feat: reuse zlib's decoder buffer by <a href="https://github.com/Vaiz"><code>@​Vaiz</code></a> in <a href="">rust-lang/flate2-rs#532</a></li>
<li>feat: add reset method for read::GzDecoder and buffered::GzDecoder by <a href="https://github.com/Vaiz"><code>@​Vaiz</code></a> in <a href="">rust-lang/flate2-rs#534</a></li>
<li>Drop cloudflare-zlib by <a href="https://github.com/kornelski"><code>@​kornelski</code></a> in <a href="">rust-lang/flate2-rs#539</a></li>
<li>Add a wrapper for the <code>Crc</code> struct by <a href="https://github.com/MikkelPaulson"><code>@​MikkelPaulson</code></a> in <a href="">rust-lang/flate2-rs#540</a></li>
<li>Bump miniz_oxide to 0.9 by <a href="https://github.com/oscargus"><code>@​oscargus</code></a> in <a href="">rust-lang/flate2-rs#543</a></li>
<li>Upgrade miniz_oxide and add unit tests of the different flush kinds by <a href="https://github.com/fintelia"><code>@​fintelia</code></a> in <a href="">rust-lang/flate2-rs#498</a></li>
<li>Fix infinite loop in writing gzip header/footer by <a href="https://github.com/Shnatsel"><code>@​Shnatsel</code></a> in <a href="">rust-lang/flate2-rs#547</a></li>
<li>test: generate corrupt gzip fixture at runtime by <a href="https://github.com/nanookclaw"><code>@​nanookclaw</code></a> in <a href="">rust-lang/flate2-rs#550</a></li>
<li>Reject oversized gzip extra fields by <a href="https://github.com/Byron"><code>@​Byron</code></a> in <a href="">rust-lang/flate2-rs#553</a></li>
<li>Reject incomplete deflate streams at EOF by <a href="https://github.com/Guflly"><code>@​Guflly</code></a> in <a href="">rust-lang/flate2-rs#556</a></li>
<li>Include <code>README.md</code> in a private module by <a href="https://github.com/bushrat011899"><code>@​bushrat011899</code></a> in <a href="">rust-lang/flate2-rs#562</a></li>
<li>Add <code>no_std</code> support using nightly <code>alloc_io</code> by <a href="https://github.com/bushrat011899"><code>@​bushrat011899</code></a> in <a href="">rust-lang/flate2-rs#559</a></li>
<li>Update <code>get_mut()</code> documentation to make clear how 'inner` can be used by <a href="https://github.com/Byron"><code>@​Byron</code></a> in <a href="">rust-lang/flate2-rs#558</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Vaiz"><code>@​Vaiz</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#532</a></li>
<li><a href="https://github.com/MikkelPaulson"><code>@​MikkelPaulson</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#540</a></li>
<li><a href="https://github.com/oscargus"><code>@​oscargus</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#543</a></li>
<li><a href="https://github.com/nanookclaw"><code>@​nanookclaw</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#550</a></li>
<li><a href="https://github.com/Guflly"><code>@​Guflly</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#556</a></li>
<li><a href="https://github.com/bushrat011899"><code>@​bushrat011899</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#562</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.9...1.1.10">https://github.com/rust-lang/flate2-rs/compare/1.1.9...1.1.10</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ed93d4f</code></a> Merge pull request <a href="">#558</a> from rust-lang/lib-doc-update</li>
<li><a href=""><code>fb5228d</code></a> Merge pull request <a href="">#559</a> from bushrat011899/no_std</li>
<li><a href=""><code>6ed3ba3</code></a> Add executable <code>no_std</code> example</li>
<li><a href=""><code>faed8a0</code></a> Expand CI to test <code>no_std</code> compatibility and correctness</li>
<li><a href=""><code>2ba8e7e</code></a> Add unstable <code>no_std</code> support behind <code>flate2_unstable_nightly_alloc_io</code></li>
<li><a href=""><code>3fe1126</code></a> Centralize usage of <code>std</code> for <code>error</code> and <code>io</code></li>
<li><a href=""><code>98e313a</code></a> Add <code>GzHeader::mtime_as_duration</code></li>
<li><a href=""><code>0642965</code></a> Switch to <code>core</code> implicit prelude and only use <code>std</code> where required</li>
<li><a href=""><code>454a63c</code></a> Remove left-over <code>dbg!</code> statement</li>
<li><a href=""><code>2a490b7</code></a> Add <code>runtime_detection</code> feature</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.9...1.1.10">compare view</a></li>
</ul>
</details>
<br />

Updates `gzp` from 2.0.3 to 2.0.4
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sstadick/gzp/blob/main/CHANGELOG.md">gzp's changelog</a>.</em></p>
<blockquote>
<h1>v2.0.4</h1>
<ul>
<li>chore: Refresh <code>bytes</code>, <code>thiserror</code>, <code>libdeflater</code>, <code>proptest</code>, and <code>tempfile</code>, and move the lockfile off the yanked <code>spin</code> 0.9.8 release.</li>
<li>chore: Update the pinned <code>actions/checkout</code> workflow action to v7.0.1.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cb76904</code></a> release: prepare v2.0.4 (<a href="">#78</a>)</li>
<li>See full diff in <a href="https://github.com/sstadick/gzp/compare/v2.0.3...v2.0.4">compare view</a></li>
</ul>
</details>
<br />

Updates `log` from 0.4.33 to 0.4.35
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/log/releases">log's releases</a>.</em></p>
<blockquote>
<h2>v0.4.35</h2>
<p>This release doesn't include source changes. It verifies <code>log</code>'s new CI/CD processes.</p>
<h3>Other</h3>
<ul>
<li>rework CI/CD to align with Rust project standards</li>
</ul>
<h2>0.4.34</h2>
<h2>What's Changed</h2>
<ul>
<li>doc: Add context-logger utility to README by <a href="https://github.com/alekseysidorov"><code>@​alekseysidorov</code></a> in <a href="">rust-lang/log#735</a></li>
<li>Add alloc support for boxed loggers by <a href="https://github.com/malezjaa"><code>@​malezjaa</code></a> in <a href="">rust-lang/log#737</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/alekseysidorov"><code>@​alekseysidorov</code></a> made their first contribution in <a href="">rust-lang/log#735</a></li>
<li><a href="https://github.com/malezjaa"><code>@​malezjaa</code></a> made their first contribution in <a href="">rust-lang/log#737</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.33...0.4.34">https://github.com/rust-lang/log/compare/0.4.33...0.4.34</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/log/blob/main/CHANGELOG.md">log's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/rust-lang/log/compare/v0.4.34...v0.4.35">0.4.35</a> - 2026-10-30</h2>
<p>This release doesn't include source changes. It verifies <code>log</code>'s new CI/CD processes.</p>
<h3>Other</h3>
<ul>
<li>rework CI/CD to align with Rust project standards</li>
</ul>
<h2>[0.4.34] - 2026-08-22</h2>
<h2>What's Changed</h2>
<ul>
<li>doc: Add context-logger utility to README by <a href="https://github.com/alekseysidorov"><code>@​alekseysidorov</code></a> in <a href="">rust-lang/log#735</a></li>
<li>Add alloc support for boxed loggers by <a href="https://github.com/malezjaa"><code>@​malezjaa</code></a> in <a href="">rust-lang/log#737</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/alekseysidorov"><code>@​alekseysidorov</code></a> made their first contribution in <a href="">rust-lang/log#735</a></li>
<li><a href="https://github.com/malezjaa"><code>@​malezjaa</code></a> made their first contribution in <a href="">rust-lang/log#737</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.33...0.4.34">https://github.com/rust-lang/log/compare/0.4.33...0.4.34</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a46450b</code></a> Update CHANGELOG.md</li>
<li><a href=""><code>a715f17</code></a> chore: release v0.4.35</li>
<li><a href=""><code>b4e2b12</code></a> Merge pull request <a href="">#747</a> from rust-lang/chore/release-plz-mgnt</li>
<li><a href=""><code>6b490b6</code></a> run fmt</li>
<li><a href=""><code>2c7fd52</code></a> simplify some crate release tasks for easier automation</li>
<li><a href=""><code>5bc5545</code></a> Merge pull request <a href="">#745</a> from marcoienibot/release-plz-disable-semver-check</li>
<li><a href=""><code>4234b8c</code></a> Disable release-plz semver check</li>
<li><a href=""><code>95918ff</code></a> Merge pull request <a href="">#744</a> from Kobzol/trusted-publishing</li>
<li><a href=""><code>e7ed747</code></a> Fix Zizmor lints</li>
<li><a href=""><code>e87a3c6</code></a> Setup trusted publishing</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/log/compare/0.4.33...v0.4.35">compare view</a></li>
</ul>
</details>
<br />

Updates `serde_json` from 1.0.151 to 1.0.154
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/serde-rs/json/releases">serde_json's releases</a>.</em></p>
<blockquote>
<h2>v1.0.154</h2>
<ul>
<li>Support preserve_order in no_std builds (<a href="">#1333</a>, thanks <a href="https://github.com/razmser"><code>@​razmser</code></a>)</li>
</ul>
<h2>v1.0.153</h2>
<ul>
<li>Report invalid UTF-8 at the first bad byte (<a href="">#1345</a>, thanks <a href="https://github.com/00200200"><code>@​00200200</code></a>)</li>
</ul>
<h2>v1.0.152</h2>
<ul>
<li>Preserve sign of <code>-0</code> in arbitrary_precision mode (<a href="">#1346</a>, thanks <a href="https://github.com/yuxi-liu-wired"><code>@​yuxi-liu-wired</code></a>)</li>
<li>Fix comparison of large non-integer values with f32::INFINITY (<a href="">#1347</a>, thanks <a href="https://github.com/yuxi-liu-wired"><code>@​yuxi-liu-wired</code></a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>20572a6</code></a> Release 1.0.154</li>
<li><a href=""><code>a91bfaf</code></a> Fix RandomState links in map documentation</li>
<li><a href=""><code>3c932c0</code></a> Merge pull request <a href="">#1333</a> from razmser/no-std-preserve-order</li>
<li><a href=""><code>4b2d726</code></a> Release 1.0.153</li>
<li><a href=""><code>83335ee</code></a> Touch up PR 1345</li>
<li><a href=""><code>4b4810a</code></a> Resolve range_plus_one pedantic clippy lint</li>
<li><a href=""><code>8af71cc</code></a> Merge pull request <a href="">#1345</a> from 00200200/fix-invalid-utf8-error-column</li>
<li><a href=""><code>452afa2</code></a> Correct multiline raw UTF-8 error positions and simplify indexing</li>
<li><a href=""><code>c9f1e3b</code></a> Release 1.0.152</li>
<li><a href=""><code>854fc70</code></a> Touch up PR 1347</li>
<li>Additional commits viewable in <a href="https://github.com/serde-rs/json/compare/v1.0.151...v1.0.154">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d252ea159f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.