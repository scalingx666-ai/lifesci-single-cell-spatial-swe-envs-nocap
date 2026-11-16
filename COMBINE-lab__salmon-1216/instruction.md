# Issue

**Title:** chore(deps): bump the cargo-patch group across 1 directory with 5 updates

## Description

Bumps the cargo-patch group with 5 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [crossbeam](https://github.com/crossbeam-rs/crossbeam) | `0.8.4` | `0.8.5` |
| [crossbeam-channel](https://github.com/crossbeam-rs/crossbeam) | `0.5.16` | `0.5.17` |
| [clap](https://github.com/clap-rs/clap) | `4.6.6` | `4.6.7` |
| [jiff](https://github.com/BurntSushi/jiff) | `0.2.35` | `0.2.37` |
| [crossbeam-queue](https://github.com/crossbeam-rs/crossbeam) | `0.3.13` | `0.3.14` |

Updates `crossbeam` from 0.8.4 to 0.8.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/crossbeam-rs/crossbeam/releases">crossbeam's releases</a>.</em></p>
<blockquote>
<h2>crossbeam-utils 0.8.5</h2>
<ul>
<li>Add <code>AtomicCell::fetch_update</code> (<a href="">#704</a>)</li>
<li>Support targets that do not have atomic CAS on stable Rust (<a href="">#698</a>)</li>
</ul>
<h2>crossbeam-deque 0.8.5</h2>
<ul>
<li>Remove dependency on <code>cfg-if</code>. (<a href="">#1072</a>)</li>
</ul>
<h2>crossbeam 0.8.5</h2>
<ul>
<li>Update MSRV policy to support 1 year instead of 6 months to meet rayon's MSRV policy. (<a href="">#1284</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/crossbeam-rs/crossbeam/blob/main/CHANGELOG.md">crossbeam's changelog</a>.</em></p>
<blockquote>
<h1>Version 0.8.5</h1>
<ul>
<li>Update MSRV policy to support 1 year instead of 6 months to meet rayon's MSRV policy. (<a href="">#1284</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2920c98</code></a> Prepare for the next release</li>
<li><a href=""><code>808b75a</code></a> ci: Update codegen job</li>
<li><a href=""><code>46774e0</code></a> channel: Document that send_timeout sends an available message even if the ti...</li>
<li><a href=""><code>89a3fe4</code></a> epoch: Make Shared::null const</li>
<li><a href=""><code>383d74a</code></a> Use *::MAX associated constants</li>
<li><a href=""><code>a30b825</code></a> channel,deque,queue: Use AtomicU64/u64 in head/tail index if available</li>
<li><a href=""><code>a0e4d29</code></a> Replace iterative capacity growth with <code>next_power_of_two</code> (<a href="">#1216</a>)</li>
<li><a href=""><code>94f74d2</code></a> Recognize x86_64-unknown-linux-gnutsan in build script</li>
<li><a href=""><code>30e5963</code></a> epoch: Add missing fence emulation for tsan</li>
<li><a href=""><code>708a6bd</code></a> Handle overflow in bounded channel/queue initialization (<a href="">#1301</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/crossbeam-rs/crossbeam/compare/crossbeam-0.8.4...crossbeam-0.8.5">compare view</a></li>
</ul>
</details>
<br />

Updates `crossbeam-channel` from 0.5.16 to 0.5.17
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/crossbeam-rs/crossbeam/releases">crossbeam-channel's releases</a>.</em></p>
<blockquote>
<h2>crossbeam-channel 0.5.17</h2>
<ul>
<li>Fix UB in bounded channel when <code>SelectedOperation</code> is leaked. (<a href="">#1295</a>)</li>
<li>Fix behavior inconsistency on already received case in <code>at()</code>. (<a href="">#1296</a>)</li>
<li>Handle overflow in bounded channel initialization. (<a href="">#1301</a>)</li>
<li>Use 64-bit index on 32-bit platforms if 64-bit atomic is available. (<a href="">#1321</a>)</li>
<li>Update MSRV policy to support 1 year instead of 6 months to meet rayon's MSRV policy. (<a href="">#1284</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2920c98</code></a> Prepare for the next release</li>
<li><a href=""><code>808b75a</code></a> ci: Update codegen job</li>
<li><a href=""><code>46774e0</code></a> channel: Document that send_timeout sends an available message even if the ti...</li>
<li><a href=""><code>89a3fe4</code></a> epoch: Make Shared::null const</li>
<li><a href=""><code>383d74a</code></a> Use *::MAX associated constants</li>
<li><a href=""><code>a30b825</code></a> channel,deque,queue: Use AtomicU64/u64 in head/tail index if available</li>
<li><a href=""><code>a0e4d29</code></a> Replace iterative capacity growth with <code>next_power_of_two</code> (<a href="">#1216</a>)</li>
<li><a href=""><code>94f74d2</code></a> Recognize x86_64-unknown-linux-gnutsan in build script</li>
<li><a href=""><code>30e5963</code></a> epoch: Add missing fence emulation for tsan</li>
<li><a href=""><code>708a6bd</code></a> Handle overflow in bounded channel/queue initialization (<a href="">#1301</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/crossbeam-rs/crossbeam/compare/crossbeam-channel-0.5.16...crossbeam-channel-0.5.17">compare view</a></li>
</ul>
</details>
<br />

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

Updates `jiff` from 0.2.35 to 0.2.37
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/BurntSushi/jiff/blob/jiff-static-0.2.37/CHANGELOG.md">jiff's changelog</a>.</em></p>
<blockquote>
<h1>0.2.37 (2026-09-12)</h1>
<p>This is a redux release of <code>0.2.36</code> that fixes a compilation bug.</p>
<p>Bug fixes:</p>
<ul>
<li><a href="">#647</a>:
Fixes a compilation bug due to incorrect include paths.</li>
</ul>
<h1>0.2.36 (2026-09-12)</h1>
<p>This release has a couple bug fixes and adds opt-in integration with the
<code>arbitrary</code> crate.</p>
<p>Enhancements:</p>
<ul>
<li><a href="">#631</a>:
Add optional <code>Arbitrary</code> trait implementations from the <code>arbitrary</code> crate.</li>
</ul>
<p>Bug fixes:</p>
<ul>
<li><a href="">#617</a>:
Fixes a bug in <code>jiff_core::tz::Offset</code> checked subtraction routine.</li>
<li><a href="">#627</a>:
Use <code>serialize_some</code> for optional Serde helpers in <code>jiff::fmt::serde</code>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4100a7c</code></a> 0.2.37</li>
<li><a href=""><code>c1febcb</code></a> changelog: 0.2.37</li>
<li><a href=""><code>7bd0c36</code></a> doc: fix include paths, redux</li>
<li><a href=""><code>aa8008e</code></a> Revert &quot;doc: fix include paths&quot;</li>
<li><a href=""><code>8c2585c</code></a> doc: fix include paths</li>
<li><a href=""><code>7e81331</code></a> 0.2.36</li>
<li><a href=""><code>d2f10b1</code></a> jiff-core-0.1.1</li>
<li><a href=""><code>189c390</code></a> changelog: 0.2.36</li>
<li><a href=""><code>ab6e8c8</code></a> jiff: remove duplicated docs</li>
<li><a href=""><code>eabd531</code></a> jiff: add optional <code>arbitrary::Arbitrary</code> implementations</li>
<li>Additional commits viewable in <a href="https://github.com/BurntSushi/jiff/compare/jiff-static-0.2.35...jiff-static-0.2.37">compare view</a></li>
</ul>
</details>
<br />

Updates `crossbeam-queue` from 0.3.13 to 0.3.14
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/crossbeam-rs/crossbeam/releases">crossbeam-queue's releases</a>.</em></p>
<blockquote>
<h2>crossbeam-queue 0.3.14</h2>
<ul>
<li>Use 64-bit index on 32-bit platforms if 64-bit atomic is available. (<a href="">#1321</a>)</li>
<li>Update MSRV policy to support 1 year instead of 6 months to meet rayon's MSRV policy. (<a href="">#1284</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2920c98</code></a> Prepare for the next release</li>
<li><a href=""><code>808b75a</code></a> ci: Update codegen job</li>
<li><a href=""><code>46774e0</code></a> channel: Document that send_timeout sends an available message even if the ti...</li>
<li><a href=""><code>89a3fe4</code></a> epoch: Make Shared::null const</li>
<li><a href=""><code>383d74a</code></a> Use *::MAX associated constants</li>
<li><a href=""><code>a30b825</code></a> channel,deque,queue: Use AtomicU64/u64 in head/tail index if available</li>
<li><a href=""><code>a0e4d29</code></a> Replace iterative capacity growth with <code>next_power_of_two</code> (<a href="">#1216</a>)</li>
<li><a href=""><code>94f74d2</code></a> Recognize x86_64-unknown-linux-gnutsan in build script</li>
<li><a href=""><code>30e5963</code></a> epoch: Add missing fence emulation for tsan</li>
<li><a href=""><code>708a6bd</code></a> Handle overflow in bounded channel/queue initialization (<a href="">#1301</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/crossbeam-rs/crossbeam/compare/crossbeam-queue-0.3.13...crossbeam-queue-0.3.14">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcea903bb940`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.