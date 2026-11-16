# Issue

**Title:** chore(deps-dev): bump mypy from 1.20.2 to 2.3.0

## Description

Bumps [mypy](https://github.com/python/mypy) from 1.20.2 to 2.3.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/python/mypy/blob/master/CHANGELOG.md">mypy's changelog</a>.</em></p>
<blockquote>
<h1>Mypy Release Notes</h1>
<h2>Next Release</h2>
<h3>Packaging changes</h3>
<ul>
<li>No longer provide mypyc-accelerated wheels for macOS x86_64 [mypyc-wheels <a href="">#119</a>](<a href="">mypyc/mypy_mypyc-wheels#119</a>)</li>
</ul>
<h2>Mypy 2.3</h2>
<p>We've just uploaded mypy 2.3.0 to the Python Package Index (<a href="https://pypi.org/project/mypy/">PyPI</a>).
Mypy is a static type checker for Python. This release includes new features, performance
improvements and bug fixes. You can install it as follows:</p>
<pre><code>python3 -m pip install -U mypy
</code></pre>
<p>You can read the full documentation for this release on <a href="http://mypy.readthedocs.io">Read the Docs</a>.</p>
<h3>The Upcoming Switch to the New Native Parser</h3>
<p>We are planning to enable the new native parser (<code>--native-parser</code>) by
default soon. We recommend that you test the native parser in your projects and report
any issues in the <a href="https://github.com/python/mypy/issues">mypy issue tracker</a>.</p>
<h3>Mypyc Free-threading Memory Safety</h3>
<p>Free-threaded Python builds that don't have the GIL require additional synchronization
primitives or lock-free algorithms to ensure memory safety when there are race conditions
(for example, when a thread reads a list item while another thread writes the same list
item concurrently). This release greatly improves memory safety of free threading.</p>
<p>List operations are now memory-safe on free threaded Python builds, even in the presence of
race conditions. This has some performance cost. For list-heavy workloads, using
<code>librt.vecs.vec</code> instead of list is often significantly faster, but note that <code>vec</code> is not
(and likely won't be) fully memory safe, and the user is expected to avoid race conditions.
The newly introduced <code>librt.threading.Lock</code> helps with this. Using variable-length tuples
can also be more efficient than lists, since tuples are immutable and don't require
expensive synchronization to ensure memory safety.</p>
<p>Instance attribute access is also (mostly) memory safe now on free-threaded builds in
the presence of race conditions. We are planning to fix the remaining unsafe cases in a
future release.</p>
<p>Full list of changes:</p>
<ul>
<li>Make attribute access memory safe on free-threaded builds (Jukka Lehtosalo, PR <a href="">21705</a>)</li>
<li>Fix unsafe borrowing of instance attributes with free-threading (Jukka Lehtosalo, PR <a href="">21688</a>)</li>
<li>Make list get/set item more memory safe on free-threaded builds (Jukka Lehtosalo, PR <a href="">21683</a>)</li>
<li>Don't borrow list items on free-threaded builds (Jukka Lehtosalo, PR <a href="">21679</a>)</li>
<li>Make multiple assignment from list memory-safe on free-threaded builds (Jukka Lehtosalo, PR <a href="">21684</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8aabf84</code></a> Drop +dev from version</li>
<li><a href=""><code>4d8ad2a</code></a> Update changelog for 2.3 release (<a href="">#21728</a>)</li>
<li><a href=""><code>2c21546</code></a> [mypyc] Update documentation of race conditions under free threading (<a href="">#21726</a>)</li>
<li><a href=""><code>a9f62a3</code></a> [mypyc] Make attribute access memory safe on free-threaded builds (<a href="">#21705</a>)</li>
<li><a href=""><code>0faa413</code></a> Use <code>PYODIDE</code> environment variable for Emscripten cross-compilation detection...</li>
<li><a href=""><code>3d75cdb</code></a> [mypyc] Borrow final attributes more aggressively (<a href="">#21702</a>)</li>
<li><a href=""><code>24c237d</code></a> [mypyc] Improve documentation of Final (<a href="">#21713</a>)</li>
<li><a href=""><code>b5be217</code></a> [mypyc] Update free threading Python compatibility docs (<a href="">#21711</a>)</li>
<li><a href=""><code>cbcb51a</code></a> Narrow for frozendict membership check (<a href="">#21709</a>)</li>
<li><a href=""><code>af2bc0f</code></a> Sync typeshed (<a href="">#21707</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/python/mypy/compare/v1.20.2...v2.3.0">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7164cbea7bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.