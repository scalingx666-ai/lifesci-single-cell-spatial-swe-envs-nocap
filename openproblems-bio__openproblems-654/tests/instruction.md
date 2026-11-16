# Issue

**Title:** Update rpy2 requirement from <3.5.5 to <3.5.6

## Description

Updates the requirements on [rpy2](https://github.com/rpy2/rpy2) to permit the latest version.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rpy2/rpy2/blob/master/NEWS">rpy2's changelog</a>.</em></p>
<blockquote>
<h1>Release 3.5.5</h1>
<h2>New features</h2>
<ul>
<li>
<p>For ipython and Jupyter notebooks, R &quot;magics&quot; accepting optional input arguments
(<code>-i</code> or <code>--input</code>) can now be of form <code>&lt;python-name&gt;</code> or
<code>&lt;r-name&gt;=&lt;python-name&gt;</code>. The former is the way is has been working so far:
the R object is given the name of the Python object. The latter allows to
specify the name under which the input object will be known to R. In addition
to that the python name can optionally be a path, that is a name nested in a
sequence of namespaces. For example, <code>-i module.varname</code>. The magics
concerned are <code>%R</code>, <code>%%R</code>, and <code>%Rpush</code> (issues <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/934">#934</a> and <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/935">#935</a>).</p>
</li>
<li>
<p>For ipython and Jupyter notebooks, R &quot;magics&quot; accepting an optional conversion
argument (<code>-c/--converter</code>) now also accepts names that are a path in Python,
that is a name nested in a sequence of namespaces. For example,
<code>-c rpy2.robjects.default_converter</code> (issue <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/934">#934</a>).</p>
</li>
<li>
<p>The &quot;magic&quot; <code>%Rpush</code> accepts an optional argument <code>-c/--converter</code> that is
similar in nature to the argument of the same name in <code>%R</code> and <code>%%R</code>.</p>
</li>
</ul>
<h2>Bugs fixed</h2>
<ul>
<li>
<p>:class:<code>rpy2.rlike.container.TaggedList</code> objects were triggering an error when unpickled (issue <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/947">#947</a>).</p>
</li>
<li>
<p>Converting :class:<code>pandas.Series</code> of type <code>&quot;object&quot;</code> with a fallback
to R strings no longer fails with an error (issue <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/916">#916</a>).</p>
</li>
</ul>
<h2>Changes</h2>
<ul>
<li>
<p>:meth:<code>rpy2.robjects.help.Page.iteritems</code> is deprecated. Use the method <code>items()</code> instead.</p>
</li>
<li>
<p>Calling :func:<code>str</code> on rpy2 objects that are proxies of R objects is now
using R's <code>print()</code> whenever R's <code>show()</code> results in an error (issue <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/908">#908</a>).</p>
</li>
</ul>
<h1>Release 3.5.4</h1>
<h2>New features</h2>
<ul>
<li>:func:<code>rpy2.rinterface.rternalize</code> can optionally mirror more accurately in R
the function signature defined in Python (issue <a href="https://github-redirect.dependabot.com/rpy2/rpy2/issues/905">#905</a>).</li>
</ul>
<p>Bugs fixed</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/rpy2/rpy2/commits">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fdbaad5b9d66`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.