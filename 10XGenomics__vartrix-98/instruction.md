# Issue

**Title:** Bump itertools from 0.8.0 to 0.13.0

## Description

Bumps [itertools](https://github.com/rust-itertools/itertools) from 0.8.0 to 0.13.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-itertools/itertools/blob/master/CHANGELOG.md">itertools's changelog</a>.</em></p>
<blockquote>
<h2>0.13.0</h2>
<h3>Breaking</h3>
<ul>
<li>Removed implementation of <code>DoubleEndedIterator</code> for <code>ConsTuples</code> (<a href="">#853</a>)</li>
<li>Made <code>MultiProduct</code> fused and fixed on an empty iterator (<a href="">#835</a>, <a href="">#834</a>)</li>
<li>Changed <code>iproduct!</code> to return tuples for maxi one iterator too (<a href="">#870</a>)</li>
<li>Changed <code>PutBack::put_back</code> to return the old value (<a href="">#880</a>)</li>
<li>Removed deprecated <code>repeat_call, Itertools::{foreach, step, map_results, fold_results}</code> (<a href="">#878</a>)</li>
<li>Removed <code>TakeWhileInclusive::new</code> (<a href="">#912</a>)</li>
</ul>
<h3>Added</h3>
<ul>
<li>Added <code>Itertools::{smallest_by, smallest_by_key, largest, largest_by, largest_by_key}</code> (<a href="">#654</a>, <a href="">#885</a>)</li>
<li>Added <code>Itertools::tail</code> (<a href="">#899</a>)</li>
<li>Implemented <code>DoubleEndedIterator</code> for <code>ProcessResults</code> (<a href="">#910</a>)</li>
<li>Implemented <code>Debug</code> for <code>FormatWith</code> (<a href="">#931</a>)</li>
<li>Added <code>Itertools::get</code> (<a href="">#891</a>)</li>
</ul>
<h3>Changed</h3>
<ul>
<li>Deprecated <code>Itertools::group_by</code> (renamed <code>chunk_by</code>) (<a href="">#866</a>, <a href="">#879</a>)</li>
<li>Deprecated <code>unfold</code> (use <code>std::iter::from_fn</code> instead) (<a href="">#871</a>)</li>
<li>Optimized <code>GroupingMapBy</code> (<a href="">#873</a>, <a href="">#876</a>)</li>
<li>Relaxed <code>Fn</code> bounds to <code>FnMut</code> in <code>diff_with, Itertools::into_group_map_by</code> (<a href="">#886</a>)</li>
<li>Relaxed <code>Debug/Clone</code> bounds for <code>MapInto</code> (<a href="">#889</a>)</li>
<li>Documented the <code>use_alloc</code> feature (<a href="">#887</a>)</li>
<li>Optimized <code>Itertools::set_from</code> (<a href="">#888</a>)</li>
<li>Removed badges in <code>README.md</code> (<a href="">#890</a>)</li>
<li>Added &quot;no-std&quot; categories in <code>Cargo.toml</code> (<a href="">#894</a>)</li>
<li>Fixed <code>Itertools::k_smallest</code> on short unfused iterators (<a href="">#900</a>)</li>
<li>Deprecated <code>Itertools::tree_fold1</code> (renamed <code>tree_reduce</code>) (<a href="">#895</a>)</li>
<li>Deprecated <code>GroupingMap::fold_first</code> (renamed <code>reduce</code>) (<a href="">#902</a>)</li>
<li>Fixed <code>Itertools::k_smallest(0)</code> to consume the iterator, optimized <code>Itertools::k_smallest(1)</code> (<a href="">#909</a>)</li>
<li>Specialized <code>Combinations::nth</code> (<a href="">#914</a>)</li>
<li>Specialized <code>MergeBy::fold</code> (<a href="">#920</a>)</li>
<li>Specialized <code>CombinationsWithReplacement::nth</code> (<a href="">#923</a>)</li>
<li>Specialized <code>FlattenOk::{fold, rfold}</code> (<a href="">#927</a>)</li>
<li>Specialized <code>Powerset::nth</code> (<a href="">#924</a>)</li>
<li>Documentation fixes (<a href="">#882</a>, <a href="">#936</a>)</li>
<li>Fixed <code>assert_equal</code> for iterators longer than <code>i32::MAX</code> (<a href="">#932</a>)</li>
<li>Updated the <code>must_use</code> message of non-lazy <code>KMergeBy</code> and <code>TupleCombinations</code> (<a href="">#939</a>)</li>
</ul>
<h3>Notable Internal Changes</h3>
<ul>
<li>Tested iterator laziness (<a href="">#792</a>)</li>
<li>Created <code>CONTRIBUTING.md</code> (<a href="">#767</a>)</li>
</ul>
<h2>0.12.1</h2>
<h3>Added</h3>
<ul>
<li>Documented iteration order guarantee for <code>Itertools::[tuple_]combinations</code> (<a href="">#822</a>)</li>
<li>Documented possible panic in <code>iterate</code> (<a href="">#842</a>)</li>
<li>Implemented <code>Clone</code> and <code>Debug</code> for <code>Diff</code> (<a href="">#845</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d5084d1</code></a> Prepare v0.13.0 release (<a href="">#937</a>)</li>
<li><a href=""><code>d7c99d5</code></a> <code>TupleCombinations</code> is not lazy but must be used nonetheless</li>
<li><a href=""><code>074c7fc</code></a> <code>KMergeBy</code> is not lazy but must be used nonetheless</li>
<li><a href=""><code>2ad9e07</code></a> <code>assert_equal</code>: fix <code>clippy::default_numeric_fallback</code></li>
<li><a href=""><code>0d4efc8</code></a> Remove free function <code>get</code></li>
<li><a href=""><code>05cc0ee</code></a> <code>get(s..=usize::MAX)</code> should be fine when <code>s != 0</code></li>
<li><a href=""><code>3c16f14</code></a> <code>get</code>: when is it ESI and/or DEI</li>
<li><a href=""><code>4dd6ba0</code></a> <code>get</code>: panics if the range includes <code>usize::MAX</code></li>
<li><a href=""><code>7a9ce56</code></a> <code>get(r: Range)</code> as <code>Skip\&lt;Take&gt;</code></li>
<li><a href=""><code>f676f2f</code></a> Remove the unspecified check about <code>.get(exhausted_range_inclusive)</code></li>
<li>Additional commits viewable in <a href="https://github.com/rust-itertools/itertools/compare/0.8.0...v0.13.0">compare view</a></li>
</ul>
</details>
<br />

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4176e99ad7c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.