# Issue

**Title:** Bump rayon from 1.7.0 to 1.12.0

## Description

Bumps [rayon](https://github.com/rayon-rs/rayon) from 1.7.0 to 1.12.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rayon-rs/rayon/blob/main/RELEASES.md">rayon's changelog</a>.</em></p>
<blockquote>
<h1>Release rayon 1.12.0 (2026-04-13)</h1>
<ul>
<li>Fixed a bug in parallel <code>Range&lt;char&gt;</code> when the end is 0xE000, just past the
surrogate boundary, which was unsafely producing invalid <code>char</code> values.</li>
<li>The new method <code>ParallelSlice::par_array_windows</code> works like <code>par_windows</code>
but with a constant length, producing <code>&amp;[T; N]</code> items.</li>
</ul>
<h1>Release rayon 1.11.0 / rayon-core 1.13.0 (2025-08-12)</h1>
<ul>
<li>The minimum supported <code>rustc</code> is now 1.80.</li>
<li><code>iter::repeatn</code> has been renamed to <code>iter::repeat_n</code> to match the name
stabilized in the standard library. The old name still exists as a deprecated
function for compatibility.</li>
<li>Fixed a bug in <code>in_place_scope</code> when the default global registry uses the
current thread, like on WebAssembly without threading support.</li>
<li><code>binary_heap::Iter</code> no longer requires a temporary allocation.</li>
<li>Relaxed trait bounds on many of the public structs.</li>
<li>Implemented <code>IntoParallelIterator for Box&lt;[T]&gt;</code> and its references.</li>
<li>Implemented <code>FromParallelIterator&lt;_&gt; for Box&lt;str&gt;</code> via <code>String</code>.</li>
</ul>
<h1>Release rayon 1.10.0 (2024-03-23)</h1>
<ul>
<li>The new methods <code>ParallelSlice::par_chunk_by</code> and
<code>ParallelSliceMut::par_chunk_by_mut</code> work like the slice methods <code>chunk_by</code>
and <code>chunk_by_mut</code> added in Rust 1.77.</li>
</ul>
<h1>Release rayon 1.9.0 (2024-02-27)</h1>
<ul>
<li>The new methods <code>IndexedParallelIterator::by_exponential_blocks</code> and
<code>by_uniform_blocks</code> allow processing items in smaller groups at a time.</li>
<li>The new <code>iter::walk_tree</code>, <code>walk_tree_prefix</code>, and <code>walk_tree_postfix</code>
functions enable custom parallel iteration over tree-like structures.</li>
<li>The new method <code>ParallelIterator::collect_vec_list</code> returns items as a linked
list of vectors, which is an efficient mode of parallel collection used by
many of the internal implementations of <code>collect</code>.</li>
<li>The new methods <code>ParallelSliceMut::par_split_inclusive_mut</code>,
<code>ParallelSlice::par_split_inclusive</code>, and
<code>ParallelString::par_split_inclusive</code> all work like a normal split but
keeping the separator as part of the left slice.</li>
<li>The new <code>ParallelString::par_split_ascii_whitespace</code> splits only on ASCII
whitespace, which is faster than including Unicode multi-byte whitespace.</li>
<li><code>OsString</code> now implements <code>FromParallelIterator&lt;_&gt;</code> and <code>ParallelExtend&lt;_&gt;</code>
for a few item types similar to the standard <code>FromIterator</code> and <code>Extend</code>.</li>
<li>The internal <code>Pattern</code> trait for string methods is now implemented for
<code>[char; N]</code> and <code>&amp;[char; N]</code>, matching any of the given characters.</li>
</ul>
<h1>Release rayon 1.8.1 / rayon-core 1.12.1 (2024-01-17)</h1>
<ul>
<li>The new <code>&quot;web_spin_lock&quot;</code> crate feature makes mutexes spin on the main
browser thread in WebAssembly, rather than suffer an error about forbidden</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7449d7d</code></a> Merge <a href="">#1093</a></li>
<li><a href=""><code>b3d9e3f</code></a> Release rayon 1.8.0 and rayon-core 1.12.0</li>
<li><a href=""><code>3fe51e5</code></a> Fix clippy::let_and_return</li>
<li><a href=""><code>082f215</code></a> Merge <a href="">#1087</a></li>
<li><a href=""><code>ea0c06d</code></a> core: registry: Factor out &quot;wait till out of work&quot; part of the main loop.</li>
<li><a href=""><code>75524e2</code></a> Merge <a href="">#1063</a></li>
<li><a href=""><code>01d2800</code></a> Ignore the multi-threaded test on emscripten/wasm</li>
<li><a href=""><code>40b59c0</code></a> core: Make use_current_thread error rather than panic when already in the pool.</li>
<li><a href=""><code>f4db4d7</code></a> core: tests: Add some basic tests for ThreadPoolBuilder::use_current_thread.</li>
<li><a href=""><code>87274ad</code></a> core: registry: Add some more documentation for ThreadPoolBuilder::use_curren...</li>
<li>Additional commits viewable in <a href="https://github.com/rayon-rs/rayon/compare/rayon-core-v1.7.0...rayon-core-v1.12.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rayon&package-manager=cargo&previous-version=1.7.0&new-version=1.12.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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