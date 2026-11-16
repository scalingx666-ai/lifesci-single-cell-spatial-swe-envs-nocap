# Issue

**Title:** Bump rayon from 1.2.0 to 1.7.0

## Description

Bumps [rayon](https://github.com/rayon-rs/rayon) from 1.2.0 to 1.7.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rayon-rs/rayon/blob/master/RELEASES.md">rayon's changelog</a>.</em></p>
<blockquote>
<h1>Release rayon 1.7.0 / rayon-core 1.11.0 (2023-03-03)</h1>
<ul>
<li>The minimum supported <code>rustc</code> is now 1.59.</li>
<li>Added a fallback when threading is unsupported.</li>
<li>The new <code>ParallelIterator::take_any</code> and <code>skip_any</code> methods work like
unordered <code>IndexedParallelIterator::take</code> and <code>skip</code>, counting items in
whatever order they are visited in parallel.</li>
<li>The new <code>ParallelIterator::take_any_while</code> and <code>skip_any_while</code> methods work
like unordered <code>Iterator::take_while</code> and <code>skip_while</code>, which previously had
no parallel equivalent. The &quot;while&quot; condition may be satisfied from anywhere
in the parallel iterator, affecting all future items regardless of position.</li>
<li>The new <code>yield_now</code> and <code>yield_local</code> functions will cooperatively yield
execution to Rayon, either trying to execute pending work from the entire
pool or from just the local deques of the current thread, respectively.</li>
</ul>
<h1>Release rayon-core 1.10.2 (2023-01-22)</h1>
<ul>
<li>Fixed miri-reported UB for SharedReadOnly tags protected by a call.</li>
</ul>
<h1>Release rayon 1.6.1 (2022-12-09)</h1>
<ul>
<li>Simplified <code>par_bridge</code> to only pull one item at a time from the iterator,
without batching. Threads that are waiting for iterator items will now block
appropriately rather than spinning CPU. (Thanks <a href="https://github.com/njaard"><code>@​njaard</code></a>!)</li>
<li>Added protection against recursion in <code>par_bridge</code>, so iterators that also
invoke rayon will not cause mutex recursion deadlocks.</li>
</ul>
<h1>Release rayon-core 1.10.1 (2022-11-18)</h1>
<ul>
<li>Fixed a race condition with threads going to sleep while a broadcast starts.</li>
</ul>
<h1>Release rayon 1.6.0 / rayon-core 1.10.0 (2022-11-18)</h1>
<ul>
<li>The minimum supported <code>rustc</code> is now 1.56.</li>
<li>The new <code>IndexedParallelIterator::fold_chunks</code> and <code>fold_chunks_with</code> methods
work like <code>ParallelIterator::fold</code> and <code>fold_with</code> with fixed-size chunks of
items. This may be useful for predictable batching performance, without the
allocation overhead of <code>IndexedParallelIterator::chunks</code>.</li>
<li>New &quot;broadcast&quot; methods run a given function on all threads in the pool.
These run at a sort of reduced priority after each thread has exhausted their
local work queue, but before they attempt work-stealing from other threads.
<ul>
<li>The global <code>broadcast</code> function and <code>ThreadPool::broadcast</code> method will
block until completion, returning a <code>Vec</code> of all return values.</li>
<li>The global <code>spawn_broadcast</code> function and methods on <code>ThreadPool</code>, <code>Scope</code>,
and <code>ScopeFifo</code> will run detached, without blocking the current thread.</li>
</ul>
</li>
<li>Panicking methods now use <code>#[track_caller]</code> to report the caller's location.</li>
<li>Fixed a truncated length in <code>vec::Drain</code> when given an empty range.</li>
</ul>
<h2>Contributors</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7ffaf34</code></a> Merge <a href="">#716</a></li>
<li><a href=""><code>163003e</code></a> bump the release date</li>
<li><a href=""><code>f7d7553</code></a> Release rayon 1.3.0 / rayon-core 1.7.0</li>
<li><a href=""><code>b98bb23</code></a> Remove unneeded extern crate statements</li>
<li><a href=""><code>9b92c7d</code></a> cargo fmt</li>
<li><a href=""><code>e02f439</code></a> Remove useless 'use crate;' in favor of the crate prelude</li>
<li><a href=""><code>a1db0fe</code></a> Fix clippy::flat_map_identity</li>
<li><a href=""><code>4e40256</code></a> Update ci/compat-Cargo.lock</li>
<li><a href=""><code>1f9d117</code></a> Remove cfg(rayon_unstable)</li>
<li><a href=""><code>198ca7f</code></a> Remove rayon-futures</li>
<li>Additional commits viewable in <a href="https://github.com/rayon-rs/rayon/compare/v1.2.0...rayon-core-v1.7.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rayon&package-manager=cargo&previous-version=1.2.0&new-version=1.7.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea6a3eb721f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.