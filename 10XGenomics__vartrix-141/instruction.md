# Issue

**Title:** Bump itertools from 0.13.0 to 0.15.0

## Description

Bumps [itertools](https://github.com/rust-itertools/itertools) from 0.13.0 to 0.15.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-itertools/itertools/blob/master/CHANGELOG.md">itertools's changelog</a>.</em></p>
<blockquote>
<h2>0.15.0</h2>
<h3>Breaking</h3>
<ul>
<li>Restructure <code>Position</code> as struct instead of enum (<a href="">#1042</a>, <a href="">#1043</a>)</li>
<li>Canonicalize <code>all_equal_value</code>'s error type (<a href="">#1032</a>)</li>
</ul>
<h3>Added</h3>
<ul>
<li>Add <code>*_with_hasher</code> adaptors (<a href="">#1007</a>)</li>
<li>Add strip_prefix and strip_prefix_by methods (<a href="">#1104</a>)</li>
</ul>
<h3>Changed</h3>
<ul>
<li>Remove <code>Clone</code> bounds from <code>tuple_combinations</code> and <code>array_combinations</code>(<a href="">#1011</a>)</li>
<li><code>must_use</code> for <code>collect_vec</code> (<a href="">#1009</a>)</li>
<li>Make <code>izip!</code> temporary friendly (<a href="">#1021</a>)</li>
<li>Add <code>array_combinations_with_replacement</code> (<a href="">#1033</a>)</li>
<li>Implement <code>Debug</code> for remaining public types (<a href="">#1038</a>)</li>
<li>Specialize <code>ExactlyOneError::count</code> (<a href="">#1046</a>)</li>
<li>Implement <code>PeekingNext</code> for more types, in particular <code>vec::IntoIter</code> (<a href="">#1059</a>, <a href="">#1073</a>)</li>
<li>Fix <code>PadUsing::next_back</code> (<a href="">#1082</a>)</li>
<li>Introduce <code>[circular_]array_windows</code>, deprecate <code>tuple_windows</code> (<a href="">#1086</a>)</li>
<li>Deprecate <code>tuple_combinations</code> (replaced by <code>array_combinations</code>) (<a href="">#1085</a>)</li>
</ul>
<h3>Notable Internal Changes</h3>
<ul>
<li>Make <code>into_group_map</code> code more idiomatic (<a href="">#1027</a>)</li>
<li>Fix clippy lints (<a href="">#1017</a>, <a href="">#1029</a>, <a href="">#1076</a>, <a href="">#1099</a>)</li>
</ul>
<h2>0.14.0</h2>
<h3>Breaking</h3>
<ul>
<li>Increased MSRV to 1.63.0 (<a href="">#960</a>)</li>
<li>Removed generic parameter from <code>cons_tuples</code> (<a href="">#988</a>)</li>
</ul>
<h3>Added</h3>
<ul>
<li>Added <code>array_combinations</code> (<a href="">#991</a>)</li>
<li>Added <code>k_smallest_relaxed</code> and variants (<a href="">#925</a>)</li>
<li>Added <code>next_array</code> and <code>collect_array</code> (<a href="">#560</a>)</li>
<li>Implemented <code>DoubleEndedIterator</code> for <code>FilterOk</code> (<a href="">#948</a>)</li>
<li>Implemented <code>DoubleEndedIterator</code> for <code>FilterMapOk</code> (<a href="">#950</a>)</li>
</ul>
<h3>Changed</h3>
<ul>
<li>Allow <code>Q: ?Sized</code> in <code>Itertools::contains</code> (<a href="">#971</a>)</li>
<li>Improved hygiene of <code>chain!</code> (<a href="">#943</a>)</li>
<li>Improved <code>into_group_map_by</code> documentation (<a href="">#1000</a>)</li>
<li>Improved <code>tree_reduce</code> documentation (<a href="">#955</a>)</li>
<li>Improved discoverability of <code>merge_join_by</code> (<a href="">#966</a>)</li>
<li>Improved discoverability of <code>take_while_inclusive</code> (<a href="">#972</a>)</li>
<li>Improved documentation of <code>find_or_last</code> and <code>find_or_first</code> (<a href="">#984</a>)</li>
<li>Prevented exponentially large type sizes in <code>tuple_combinations</code> (<a href="">#945</a>)</li>
<li>Added <code>track_caller</code> attr for <code>asser_equal</code> (<a href="">#976</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>37bd72a</code></a> Update CHANGELOG.md: strip_prefix[_by]</li>
<li><a href=""><code>86ec635</code></a> Use <code>ControlFlow</code> in <code>fold_while</code> implementation</li>
<li><a href=""><code>d5897f7</code></a> refactor(strip_prefix): use try_for_each and drop PartialEq, Eq on StripPrefi...</li>
<li><a href=""><code>b2a978a</code></a> feat(Itertools): add strip_prefix and strip_prefix_by methods</li>
<li><a href=""><code>12b6ec6</code></a> Update CHANGELOG.md for all_equal_value_error's error type</li>
<li><a href=""><code>121821e</code></a> AllEqualValueError implements std::error::Error</li>
<li><a href=""><code>adac44e</code></a> Introduce AllEqualValueError</li>
<li><a href=""><code>5707384</code></a> Update CHANGELOG.md</li>
<li><a href=""><code>df60ff0</code></a> Update CHANGELOG.md</li>
<li><a href=""><code>113b850</code></a> Update CHANGELOG.md to include with_hasher</li>
<li>Additional commits viewable in <a href="https://github.com/rust-itertools/itertools/compare/v0.13.0...v0.15.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=itertools&package-manager=cargo&previous-version=0.13.0&new-version=0.15.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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