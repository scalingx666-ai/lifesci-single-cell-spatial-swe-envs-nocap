# Issue

**Title:** build(deps): bump the cargo-patch-minor group across 1 directory with 3 updates

## Description

Bumps the cargo-patch-minor group with 3 updates in the / directory: [memchr](https://github.com/BurntSushi/memchr), [log](https://github.com/rust-lang/log) and [serde_json](https://github.com/serde-rs/json).

Updates `memchr` from 2.8.0 to 2.8.1
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ff7dca7</code></a> 2.8.1</li>
<li><a href=""><code>016878a</code></a> target: fix aarch64_be endianness bug</li>
<li><a href=""><code>ee18717</code></a> docs: add AI policy for contributors</li>
<li><a href=""><code>db1a77d</code></a> build(deps): bump actions/checkout in the actions group (<a href="">#212</a>)</li>
<li><a href=""><code>c8abbe1</code></a> Hash-pin all actions, drop persisted credentials (<a href="">#210</a>)</li>
<li><a href=""><code>24f5daa</code></a> lint: fix clippy <code>get_first</code></li>
<li><a href=""><code>1708355</code></a> lint: fix clippy <code>question_mark</code></li>
<li><a href=""><code>5b86d0c</code></a> lint: fix clippy <code>clone_on_copy</code></li>
<li>See full diff in <a href="https://github.com/BurntSushi/memchr/compare/2.8.0...2.8.1">compare view</a></li>
</ul>
</details>
<br />

Updates `log` from 0.4.29 to 0.4.32
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/log/releases">log's releases</a>.</em></p>
<blockquote>
<h2>0.4.32</h2>
<h2>What's Changed</h2>
<ul>
<li>Support <code>Value</code> -&gt; string conversions with <code>kv</code> + <code>std</code> features instead of <code>kv_std</code> by <a href="https://github.com/tisonkun"><code>@​tisonkun</code></a> in <a href="">rust-lang/log#729</a></li>
<li>Prepare for 0.4.32 release by <a href="https://github.com/KodrAus"><code>@​KodrAus</code></a> in <a href="">rust-lang/log#730</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.31...0.4.32">https://github.com/rust-lang/log/compare/0.4.31...0.4.32</a></p>
<h2>0.4.31</h2>
<h2>What's Changed</h2>
<ul>
<li>fix typos in kv compile errors and log documentation by <a href="https://github.com/Isvane"><code>@​Isvane</code></a> in <a href="">rust-lang/log#726</a></li>
<li>Leverage static str key when possible by <a href="https://github.com/tisonkun"><code>@​tisonkun</code></a> in <a href="">rust-lang/log#727</a></li>
<li>Prepare for 0.4.31 release by <a href="https://github.com/KodrAus"><code>@​KodrAus</code></a> in <a href="">rust-lang/log#728</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Isvane"><code>@​Isvane</code></a> made their first contribution in <a href="">rust-lang/log#726</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.30...0.4.31">https://github.com/rust-lang/log/compare/0.4.30...0.4.31</a></p>
<h2>0.4.30</h2>
<h3>What's Changed</h3>
<ul>
<li>Support capturing of <code>std::net</code> types by <a href="https://github.com/KodrAus"><code>@​KodrAus</code></a> in <a href="">rust-lang/log#724</a></li>
</ul>
<h3>New Contributors</h3>
<ul>
<li><a href="https://github.com/V0ldek"><code>@​V0ldek</code></a> made their first contribution in <a href="">rust-lang/log#720</a></li>
<li><a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> made their first contribution in <a href="">rust-lang/log#723</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.29...0.4.30">https://github.com/rust-lang/log/compare/0.4.29...0.4.30</a></p>
<h3>Notable Changes</h3>
<ul>
<li>MSRV is bumped to 1.71.0 in <a href="">rust-lang/log#723</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/log/blob/master/CHANGELOG.md">log's changelog</a>.</em></p>
<blockquote>
<h2>[0.4.32] - 2026-06-04</h2>
<h3>What's Changed</h3>
<ul>
<li>Support <code>Value</code> -&gt; string conversions with <code>kv</code> + <code>std</code> features instead of <code>kv_std</code> by <a href="https://github.com/tisonkun"><code>@​tisonkun</code></a> in <a href="">rust-lang/log#729</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.31...0.4.32">https://github.com/rust-lang/log/compare/0.4.31...0.4.32</a></p>
<h2>[0.4.31] - 2026-06-02</h2>
<h3>What's Changed</h3>
<ul>
<li>Leverage static str key when possible by <a href="https://github.com/tisonkun"><code>@​tisonkun</code></a> in <a href="">rust-lang/log#727</a></li>
</ul>
<h3>New Contributors</h3>
<ul>
<li><a href="https://github.com/Isvane"><code>@​Isvane</code></a> made their first contribution in <a href="">rust-lang/log#726</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.30...0.4.31">https://github.com/rust-lang/log/compare/0.4.30...0.4.31</a></p>
<h2>[0.4.30] - 2026-05-21</h2>
<h3>What's Changed</h3>
<ul>
<li>Support capturing of <code>std::net</code> types by <a href="https://github.com/KodrAus"><code>@​KodrAus</code></a> in <a href="">rust-lang/log#724</a></li>
</ul>
<h3>New Contributors</h3>
<ul>
<li><a href="https://github.com/V0ldek"><code>@​V0ldek</code></a> made their first contribution in <a href="">rust-lang/log#720</a></li>
<li><a href="https://github.com/woodruffw"><code>@​woodruffw</code></a> made their first contribution in <a href="">rust-lang/log#723</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/log/compare/0.4.29...0.4.30">https://github.com/rust-lang/log/compare/0.4.29...0.4.30</a></p>
<h3>Notable Changes</h3>
<ul>
<li>MSRV is bumped to 1.71.0 in <a href="">rust-lang/log#723</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a5b5b21</code></a> Merge pull request <a href="">#730</a> from rust-lang/cargo/0.4.32</li>
<li><a href=""><code>c8d3b12</code></a> prepare for 0.4.32 release</li>
<li><a href=""><code>ce6cd9f</code></a> Merge pull request <a href="">#729</a> from tisonkun/kv-std-support</li>
<li><a href=""><code>20b3b05</code></a> drop cfg-feature=kv as it is already met</li>
<li><a href=""><code>7bc1200</code></a> kv::std_support may not need value-bag</li>
<li><a href=""><code>5808392</code></a> Merge pull request <a href="">#728</a> from rust-lang/cargo/0.4.31</li>
<li><a href=""><code>86d739f</code></a> prepare for 0.4.31 release</li>
<li><a href=""><code>c906cfb</code></a> Merge pull request <a href="">#727</a> from tisonkun/leverage-static-str-key-when-possible</li>
<li><a href=""><code>756c279</code></a> leverage str literal as well</li>
<li><a href=""><code>3dd250d</code></a> rename Key::from_static_str to from_str_static</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/log/compare/0.4.29...0.4.32">compare view</a></li>
</ul>
</details>
<br />

Updates `serde_json` from 1.0.149 to 1.0.150
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/serde-rs/json/releases">serde_json's releases</a>.</em></p>
<blockquote>
<h2>v1.0.150</h2>
<ul>
<li>Reject non-string enum object keys (<a href="">#1324</a>, thanks <a href="https://github.com/puneetdixit200"><code>@​puneetdixit200</code></a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a1ae73a</code></a> Release 1.0.150</li>
<li><a href=""><code>1a360b0</code></a> Merge pull request <a href="">#1324</a> from puneetdixit200/reject-non-string-enum-keys</li>
<li><a href=""><code>2037b63</code></a> Reject non-string enum object keys</li>
<li><a href=""><code>5d30df6</code></a> Resolve manual_assert_eq pedantic clippy lint</li>
<li><a href=""><code>dc8003a</code></a> Raise required compiler for preserve_order feature to 1.85</li>
<li><a href=""><code>a42fa98</code></a> Unpin CI miri toolchain</li>
<li><a href=""><code>684a60e</code></a> Pin CI miri to nightly-2026-02-11</li>
<li><a href=""><code>7c7da33</code></a> Raise required compiler to Rust 1.71</li>
<li><a href=""><code>acf4850</code></a> Simplify Number::is_f64</li>
<li><a href=""><code>6b8ceab</code></a> Resolve unnecessary_map_or clippy lint</li>
<li>Additional commits viewable in <a href="https://github.com/serde-rs/json/compare/v1.0.149...v1.0.150">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d35184bf2063`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.