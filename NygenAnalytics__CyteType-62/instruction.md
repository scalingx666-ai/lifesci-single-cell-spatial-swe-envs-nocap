# Issue

**Title:** Add require_artifacts flag and LLM validation error

## Description

### **User description**
Bump version to 0.15.0. Introduce a require_artifacts parameter to CyteType.run (default True) so callers can choose whether artifact build/upload failures should abort the run; when False the run continues without uploaded_files and logs a warning. Add LLMValidationError and map the API error code LLM_VALIDATION_FAILED to this exception, and export it from the api package. Add tests covering artifact-failure behavior (raising by default and continuing when require_artifacts=False).

___

### **PR Type**
Enhancement, Tests

___

### **Description**
- Add `require_artifacts` parameter to `CyteType.run()` to control artifact failure behavior

- Introduce `LLMValidationError` exception and map API error code `LLM_VALIDATION_FAILED`

- Implement graceful artifact failure handling with warning logs when `require_artifacts=False`

- Add comprehensive tests for artifact failure scenarios with both flag states

- Bump version to 0.15.0

___

### File Walkthrough

<table><thead><tr><th></th><th align="left">Relevant files</th></tr></thead><tbody><tr><td><strong>Configuration changes</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>__init__.py</strong><dd><code>Version bump to 0.15.0</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/__init__.py

- Bump version from 0.14.1 to 0.15.0

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Enhancement</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>__init__.py</strong><dd><code>Export LLMValidationError from API package</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/api/__init__.py

<ul><li>Import <code>LLMValidationError</code> from exceptions module<br> <li> Export <code>LLMValidationError</code> in public API <code>__all__</code> list</ul>

</details>

  </td>
  <td><a href="">+2/-0</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>exceptions.py</strong><dd><code>Add LLMValidationError exception and API mapping</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/api/exceptions.py

<ul><li>Add new <code>LLMValidationError</code> exception class for LLM validation failures<br> <li> Map API error code <code>LLM_VALIDATION_FAILED</code> to <code>LLMValidationError</code> in <br>error mapping dictionary</ul>

</details>

  </td>
  <td><a href="">+7/-0</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>main.py</strong><dd><code>Implement require_artifacts flag with error handling</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/main.py

<ul><li>Add <code>require_artifacts</code> parameter (default <code>True</code>) to <code>CyteType.run()</code> <br>method signature<br> <li> Add parameter documentation explaining artifact failure behavior <br>control<br> <li> Wrap artifact building/uploading in nested try-except block to handle <br>failures gracefully<br> <li> Log error with remediation instructions when <code>require_artifacts=True</code> <br>and artifact fails<br> <li> Log warning and continue without artifacts when <br><code>require_artifacts=False</code></ul>

</details>

  </td>
  <td><a href="">+23/-6</a>&nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Tests</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>test_cytetype_integration.py</strong><dd><code>Add artifact failure behavior tests</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

tests/test_cytetype_integration.py

<ul><li>Add test <code>test_cytetype_run_artifact_failure_raises_by_default()</code> <br>verifying exception is raised when artifact build fails with default <br>settings<br> <li> Add test <br><code>test_cytetype_run_artifact_failure_continues_when_not_required()</code> <br>verifying run continues without <code>uploaded_files</code> when <br><code>require_artifacts=False</code><br> <li> Both tests mock artifact build failure and verify payload handling</ul>

</details>

  </td>
  <td><a href="">+53/-0</a>&nbsp; &nbsp; </td>

</tr>
</table></td></tr></tbody></table>

___

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b18cada7325d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.