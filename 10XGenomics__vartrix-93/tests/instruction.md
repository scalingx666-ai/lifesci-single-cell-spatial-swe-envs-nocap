# Issue

**Title:** Bump itertools from 0.6.5 to 0.8.0

## Description

Bumps [itertools](https://github.com/rust-itertools/itertools) from 0.6.5 to 0.8.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-itertools/itertools/blob/master/CHANGELOG.md">itertools's changelog</a>.</em></p>
<blockquote>
<h2>0.8.0</h2>
<ul>
<li>Added new adaptor <code>.map_into()</code> for conversions using <code>Into</code> by <a href="https://github.com/vorner"><code>@​vorner</code></a></li>
<li>Improved <code>Itertools</code> docs by <a href="https://github.com/JohnHeitmann"><code>@​JohnHeitmann</code></a></li>
<li>The return type of <code>.sorted_by_by_key()</code> is now an iterator, not a Vec.</li>
<li>The return type of the <code>izip!(x, y)</code> macro with exactly two arguments is now the usual <code>Iterator::zip</code>.</li>
<li>Remove <code>.flatten()</code> in favour of std's <code>.flatten()</code></li>
<li>Deprecate <code>.foreach()</code> in favour of std's <code>.for_each()</code></li>
<li>Deprecate <code>.step()</code> in favour of std's <code>.step_by()</code></li>
<li>Deprecate <code>repeat_call</code> in favour of std's <code>repeat_with</code></li>
<li>Deprecate <code>.fold_while()</code> in favour of std's <code>.try_fold()</code></li>
<li>Require Rust 1.24 as minimal version.</li>
</ul>
<h2>0.7.11</h2>
<ul>
<li>Add convenience methods to <code>EitherOrBoth</code>, making it more similar to <code>Option</code> and <code>Either</code> by <a href="https://github.com/jethrogb"><code>@​jethrogb</code></a></li>
</ul>
<h2>0.7.10</h2>
<ul>
<li>No changes.</li>
</ul>
<h2>0.7.9</h2>
<ul>
<li>New inclusion policy: See the readme about suggesting features for std before accepting them in itertools.</li>
<li>The <code>FoldWhile</code> type now implements <code>Eq</code> and <code>PartialEq</code> by <a href="https://github.com/jturner314"><code>@​jturner314</code></a></li>
</ul>
<h2>0.7.8</h2>
<ul>
<li>Add new iterator method <code>.tree_fold1()</code> which is like <code>.fold1()</code> except items are combined in a tree structure (see its docs). By <a href="https://github.com/scottmcm"><code>@​scottmcm</code></a></li>
<li>Add more <code>Debug</code> impls by <a href="https://github.com/phimuemue"><code>@​phimuemue</code></a>: KMerge, KMergeBy, MergeJoinBy, ConsTuples, Intersperse, ProcessResults, RcIter, Tee, TupleWindows, Tee, ZipLongest, ZipEq, Zip.</li>
</ul>
<h2>0.7.7</h2>
<ul>
<li>Add new iterator method <code>.into_group_map() -&gt; HashMap&lt;K, Vec&lt;V&gt;&gt;</code> which turns an iterator of <code>(K, V)</code> elements into such a hash table, where values are grouped by key. By <a href="https://github.com/tobz1000"><code>@​tobz1000</code></a></li>
<li>Add new free function <code>flatten</code> for the <code>.flatten()</code> adaptor. <strong>NOTE:</strong> recent Rust nightlies have <code>Iterator::flatten</code> and thus a clash with our flatten adaptor. One workaround is to use the itertools <code>flatten</code> free function.</li>
</ul>
<h2>0.7.6</h2>
<ul>
<li>Add new adaptor <code>.multi_cartesian_product()</code> which is an n-ary product iterator by <a href="https://github.com/tobz1000"><code>@​tobz1000</code></a></li>
<li>Add new method <code>.sorted_by_key()</code> by <a href="https://github.com/Xion"><code>@​Xion</code></a></li>
<li>Provide simpler and faster <code>.count()</code> for <code>.unique()</code> and <code>.unique_by()</code></li>
</ul>
<h2>0.7.5</h2>
<ul>
<li><code>.multipeek()</code> now implements <code>PeekingNext</code>, by <a href="https://github.com/nicopap"><code>@​nicopap</code></a>.</li>
</ul>
<h2>0.7.4</h2>
<ul>
<li>Add new adaptor <code>.update()</code> by <a href="https://github.com/lucasem"><code>@​lucasem</code></a>; this adaptor is used to modify an element before passing it on in an iterator chain.</li>
</ul>
<h2>0.7.3</h2>
<ul>
<li>Add new method <code>.collect_tuple()</code> by <a href="https://github.com/matklad"><code>@​matklad</code></a>; it makes a tuple out of the iterator's elements if the number of them matches <strong>exactly</strong>.</li>
<li>Implement <code>fold</code> and <code>collect</code> for <code>.map_results()</code> which means it reuses the code of the standard <code>.map()</code> for these methods.</li>
</ul>
<h2>0.7.2</h2>
<ul>
<li>Add new adaptor <code>.merge_join_by</code> by <a href="https://github.com/srijs"><code>@​srijs</code></a>; a heterogeneous merge join for two ordered sequences.</li>
</ul>
<h2>0.7.1</h2>
<ul>
<li>Iterator adaptors and iterators in itertools now use the same <code>must_use</code> reminder that the standard library adaptors do, by <a href="https://github.com/matematikaedit"><code>@​matematikaedit</code></a> and <a href="https://github.com/bluss"><code>@​bluss</code></a> <em>“iterator adaptors are lazy and do nothing unless consumed”</em>.</li>
</ul>
<h2>0.7.0</h2>
<ul>
<li>Faster <code>izip!()</code> by <a href="https://github.com/krdln"><code>@​krdln</code></a>
<ul>
<li><code>izip!()</code> is now a wrapper for repeated regular <code>.zip()</code> and a single <code>.map()</code>. This means it optimizes as well as the standard library <code>.zip()</code> it uses. <strong>Note:</strong> <code>multizip</code> and <code>izip!()</code> are now different! The former has a named type but the latter optimizes better.</li>
</ul>
</li>
<li>Faster <code>.unique()</code></li>
<li><code>no_std</code> support, which is opt-in!
<ul>
<li>Many lovable features are still there without std, like <code>izip!()</code> or <code>.format()</code> or <code>.merge()</code>, but not those that use collections.</li>
</ul>
</li>
<li>Trait bounds were required up front instead of just on the type: <code>group_by</code>'s <code>PartialEq</code> by <a href="https://github.com/Phlosioneer"><code>@​Phlosioneer</code></a> and <code>repeat_call</code>'s <code>FnMut</code>.</li>
<li>Removed deprecated constructor <code>Zip::new</code> — use <code>izip!()</code> or <code>multizip()</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cd0602a</code></a> 0.8.0</li>
<li><a href=""><code>5a8f2fd</code></a> MAINT: Require Rust 1.24 as minimum version</li>
<li><a href=""><code>4986d92</code></a> DOC: Minor edits to module docs</li>
<li><a href=""><code>01f15a0</code></a> Merge <a href="">#288</a></li>
<li><a href=""><code>883d40a</code></a> map_into method</li>
<li><a href=""><code>3bf265d</code></a> Merge pull request <a href="">#321</a> from JohnHeitmann/master</li>
<li><a href=""><code>e820996</code></a> Document the trait extension behavior of Itertools a bit more clearly</li>
<li><a href=""><code>44c9654</code></a> Merge pull request <a href="">#318</a> from bluss/std-deprecations</li>
<li><a href=""><code>d2e254f</code></a> API: Fix the mystery deprecation message for Step</li>
<li><a href=""><code>602f2f6</code></a> API: Deprecate .foreach() in favour of std's .for_each()</li>
<li>Additional commits viewable in <a href="https://github.com/rust-itertools/itertools/compare/0.6.5...0.8.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=itertools&package-manager=cargo&previous-version=0.6.5&new-version=0.8.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b06e42e3add`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.