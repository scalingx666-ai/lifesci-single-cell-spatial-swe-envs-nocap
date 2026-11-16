# Issue

**Title:** [DEPENDABOT]: Bump xgboost from 1.5.0 to 1.6.1

## Description

Bumps [xgboost](https://github.com/dmlc/xgboost) from 1.5.0 to 1.6.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dmlc/xgboost/releases">xgboost's releases</a>.</em></p>
<blockquote>
<h2>1.6.1 Patch Release</h2>
<h2>v1.6.1 (2022 May 9)</h2>
<p>This is a patch release for bug fixes and Spark barrier mode support. The R package is unchanged.</p>
<h3>Experimental support for categorical data</h3>
<ul>
<li>Fix segfault when the number of samples is smaller than the number of categories. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7853">dmlc/xgboost#7853</a>)</li>
<li>Enable partition-based split for all model types. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7857">dmlc/xgboost#7857</a>)</li>
</ul>
<h3>JVM packages</h3>
<p>We replaced the old parallelism tracker with spark barrier mode to improve the robustness of the JVM package and fix the GPU training pipeline.</p>
<ul>
<li>Fix GPU training pipeline quantile synchronization. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7823">#7823</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7834">#7834</a>)</li>
<li>Use barrier model in spark package. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7836">dmlc/xgboost#7836</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7840">dmlc/xgboost#7840</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7845">dmlc/xgboost#7845</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7846">dmlc/xgboost#7846</a>)</li>
<li>Fix shared object loading on some platforms. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/pull/7844">dmlc/xgboost#7844</a>)</li>
</ul>
<h3>Artifacts</h3>
<p>You can verify the downloaded packages by running this on your Unix shell:</p>
<pre lang="sh"><code>echo &quot;&lt;hash&gt; &lt;artifact&gt;&quot; | shasum -a 256 --check
</code></pre>
<pre><code>2633f15e7be402bad0660d270e0b9a84ad6fcfd1c690a5d454efd6d55b4e395b  ./xgboost.tar.gz
</code></pre>
<h2>Release 1.6.0 stable</h2>
<h2>v1.6.0 (2022 Apr 16)</h2>
<p>After a long period of development, XGBoost v1.6.0 is packed with many new features and
improvements. We summarize them in the following sections starting with an introduction to
some major new features, then moving on to language binding specific changes including new
features and notable bug fixes for that binding.</p>
<h3>Development of categorical data support</h3>
<p>This version of XGBoost features new improvements and full coverage of experimental
categorical data support in Python and C package with tree model.  Both <code>hist</code>, <code>approx</code>
and <code>gpu_hist</code> now support training with categorical data.  Also, partition-based
categorical split is introduced in this release. This split type is first available in
LightGBM in the context of gradient boosting. The previous XGBoost release supported one-hot
split where the splitting criteria is of form <code>x \in {c}</code>, i.e. the categorical feature <code>x</code> is tested
against a single candidate. The new release allows for more expressive conditions: <code>x \in S</code>
where the categorical feature <code>x</code> is tested against multiple candidates. Moreover, it is now
possible to use any tree algorithms (<code>hist</code>, <code>approx</code>, <code>gpu_hist</code>) when creating categorical splits.
For more information, please see our tutorial on <a href="https://xgboost.readthedocs.io/en/latest/tutorials/categorical.html">categorical data</a>, along with
examples linked on that page. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7380">#7380</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7708">#7708</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7695">#7695</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7330">#7330</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7307">#7307</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7322">#7322</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7705">#7705</a>,
<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7652">#7652</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7592">#7592</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7666">#7666</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7576">#7576</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7569">#7569</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7529">#7529</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7575">#7575</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7393">#7393</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7465">#7465</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7385">#7385</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7371">#7371</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7745">#7745</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7810">#7810</a>)</p>
<p>In the future, we will continue to improve categorical data support with new features and
optimizations. Also, we are looking forward to bringing the feature beyond Python binding,
contributions and feedback are welcomed! Lastly, as a result of experimental status, the
behavior might be subject to change, especially the default value of related</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/dmlc/xgboost/blob/master/NEWS.md">xgboost's changelog</a>.</em></p>
<blockquote>
<h1>XGBoost Change Log</h1>
<p>This file records the changes in xgboost library in reverse chronological order.</p>
<h2>v1.6.0 (2022 Apr 16)</h2>
<p>After a long period of development, XGBoost v1.6.0 is packed with many new features and
improvements. We summarize them in the following sections starting with an introduction to
some major new features, then moving on to language binding specific changes including new
features and notable bug fixes for that binding.</p>
<h3>Development of categorical data support</h3>
<p>This version of XGBoost features new improvements and full coverage of experimental
categorical data support in Python and C package with tree model.  Both <code>hist</code>, <code>approx</code>
and <code>gpu_hist</code> now support training with categorical data.  Also, partition-based
categorical split is introduced in this release. This split type is first available in
LightGBM in the context of gradient boosting. The previous XGBoost release supported one-hot split where the splitting criteria is of form <code>x \in {c}</code>, i.e. the categorical feature <code>x</code> is tested against a single candidate. The new release allows for more expressive conditions: <code>x \in S</code> where the categorical feature <code>x</code> is tested against multiple candidates. Moreover, it is now possible to use any tree algorithms (<code>hist</code>, <code>approx</code>, <code>gpu_hist</code>) when creating categorical splits. For more
information, please see our tutorial on <a href="https://xgboost.readthedocs.io/en/latest/tutorials/categorical.html">categorical
data</a>, along with
examples linked on that page. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7380">#7380</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7708">#7708</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7695">#7695</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7330">#7330</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7307">#7307</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7322">#7322</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7705">#7705</a>,
<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7652">#7652</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7592">#7592</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7666">#7666</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7576">#7576</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7569">#7569</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7529">#7529</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7575">#7575</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7393">#7393</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7465">#7465</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7385">#7385</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7371">#7371</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7745">#7745</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7810">#7810</a>)</p>
<p>In the future, we will continue to improve categorical data support with new features and
optimizations. Also, we are looking forward to bringing the feature beyond Python binding,
contributions and feedback are welcomed! Lastly, as a result of experimental status, the
behavior might be subject to change, especially the default value of related
hyper-parameters.</p>
<h3>Experimental support for multi-output model</h3>
<p>XGBoost 1.6 features initial support for the multi-output model, which includes
multi-output regression and multi-label classification. Along with this, the XGBoost
classifier has proper support for base margin without to need for the user to flatten the
input. In this initial support, XGBoost builds one model for each target similar to the
sklearn meta estimator, for more details, please see our <a href="https://xgboost.readthedocs.io/en/latest/tutorials/multioutput.html">quick
introduction</a>.</p>
<p>(<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7365">#7365</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7736">#7736</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7607">#7607</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7574">#7574</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7521">#7521</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7514">#7514</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7456">#7456</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7453">#7453</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7455">#7455</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7434">#7434</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7429">#7429</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7405">#7405</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7381">#7381</a>)</p>
<h3>External memory support</h3>
<p>External memory support for both approx and hist tree method is considered feature
complete in XGBoost 1.6.  Building upon the iterator-based interface introduced in the
previous version, now both <code>hist</code> and <code>approx</code> iterates over each batch of data during
training and prediction.  In previous versions, <code>hist</code> concatenates all the batches into
an internal representation, which is removed in this version.  As a result, users can
expect higher scalability in terms of data size but might experience lower performance due
to disk IO. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7531">#7531</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7320">#7320</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7638">#7638</a>, <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7372">#7372</a>)</p>
<h3>Rewritten approx</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5d92a7d</code></a> Bump release version to 1.6.1. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7872">#7872</a>)</li>
<li><a href=""><code>c250881</code></a> [backport] Use maximum category in sketch. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7853">#7853</a>) (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7866">#7866</a>)</li>
<li><a href=""><code>b1b6246</code></a> [backport] Always use partition based categorical splits. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7857">#7857</a>) (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7865">#7865</a>)</li>
<li><a href=""><code>f4eb6b9</code></a> [backport] jvm-packages 1.6.1 (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7849">#7849</a>)</li>
<li><a href=""><code>f75c007</code></a> Make 1.6.0 release. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7813">#7813</a>)</li>
<li><a href=""><code>816e788</code></a> [backport] <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7808">#7808</a> <a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7810">#7810</a> (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7811">#7811</a>)</li>
<li><a href=""><code>3ee3b18</code></a> [doc] fix a typo in jvm/index.rst (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7806">#7806</a>) [skip ci] (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7807">#7807</a>)</li>
<li><a href=""><code>ece4dc4</code></a> [backport] Backport jvm changes to 1.6. (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7803">#7803</a>)</li>
<li><a href=""><code>67298cc</code></a> [backport] Backport JVM fixes and document update to 1.6 (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7792">#7792</a>)</li>
<li><a href=""><code>78d2312</code></a> [CI] Enable faulthandler to show details when 0xC0000005 error occurs (<a href="https://github-redirect.dependabot.com/dmlc/xgboost/issues/7771">#7771</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/dmlc/xgboost/compare/v1.5.0...v1.6.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=xgboost&package-manager=pip&previous-version=1.5.0&new-version=1.6.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca36341addd4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.