# Issue

**Title:** Retry chunk uploads and allow partial artifacts

## Description

### **User description**
Add robust retry and progress reporting for chunk uploads: import NetworkError, define retryable API codes and retry delays, retry on NetworkError/TimeoutError/APIError (certain codes), and print progress and final success/failure indicators. Update wait_for_completion to use logger.success for completed jobs. Improve log formatting (icons and colored success) via a custom _log_format and TYPE_CHECKING annotations. Change result logging to a clearer info block mapping annotation outputs to adata locations. Refactor artifact build/upload to return (uploaded, errors), handle vars.h5 and obs.duckdb as independent uploads with per-artifact try/except and warnings, and surface errors when require_artifacts=True. Adjust integration test to expect partial uploads behavior.

___

### **PR Type**
Enhancement, Bug fix

___

### **Description**
- Add retry logic for chunk uploads with exponential backoff delays

- Handle artifact uploads independently with per-artifact error tracking

- Improve logging with custom formatting (icons, colors, structured output)

- Allow partial artifact uploads when `require_artifacts=False`

___

### Diagram Walkthrough

```mermaid
flowchart LR
  A["Chunk Upload"] --> B["Retry Logic<br/>NetworkError/TimeoutError/APIError"]
  B --> C["Progress Reporting<br/>with Lock"]
  C --> D["Success/Failure Indicator"]
  E["vars.h5 Upload"] --> F["Independent Try/Except"]
  G["obs.duckdb Upload"] --> F
  F --> H["Return uploaded_ids<br/>+ errors list"]
  H --> I{require_artifacts?}
  I -->|True| J["Raise on Error"]
  I -->|False| K["Continue with Partial"]
```

<details><summary><h3>File Walkthrough</h3></summary>

<table><thead><tr><th></th><th align="left">Relevant files</th></tr></thead><tbody><tr><td><strong>Configuration changes</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>__init__.py</strong><dd><code>Version bump to 0.16.1</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/__init__.py

- Bump version from 0.16.0 to 0.16.1

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Enhancement</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>client.py</strong><dd><code>Add retry logic and progress reporting for chunk uploads</code>&nbsp; </dd></summary>
<hr>

cytetype/api/client.py

<ul><li>Import <code>NetworkError</code> exception for retry handling<br> <li> Define <code>_CHUNK_RETRY_DELAYS</code> tuple and <code>_RETRYABLE_API_ERROR_CODES</code> <br>frozenset for retry logic<br> <li> Implement retry mechanism in <code>_upload_chunk</code> with exponential backoff <br>for <code>NetworkError</code>, <code>TimeoutError</code>, and specific <code>APIError</code> codes<br> <li> Add thread-safe progress tracking with <code>_progress_lock</code> and <code>_chunks_done</code> <br>counter<br> <li> Print progress updates and colored success indicator on completion<br> <li> Ensure newline printed on upload failure</ul>

</details>

  </td>
  <td><a href="">+55/-9</a>&nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>config.py</strong><dd><code>Implement custom log formatting with icons</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/config.py

<ul><li>Add <code>TYPE_CHECKING</code> import for type hints<br> <li> Define custom <code>_log_format</code> function with emoji icons for WARNING and <br>SUCCESS levels<br> <li> Apply custom format to logger configuration for improved visual output</ul>

</details>

  </td>
  <td><a href="">+18/-2</a>&nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>results.py</strong><dd><code>Restructure results logging format</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/core/results.py

<ul><li>Change <code>logger.success</code> to <code>logger.info</code> for annotation results<br> <li> Reformat result logging message with aligned arrows and clearer <br>mapping of outputs to adata locations</ul>

</details>

  </td>
  <td><a href="">+6/-6</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>main.py</strong><dd><code>Support independent artifact uploads with error tracking</code>&nbsp; </dd></summary>
<hr>

cytetype/main.py

<ul><li>Refactor <code>_build_and_upload_artifacts</code> to return tuple of <code>(uploaded_ids, </code><br><code>errors)</code> instead of raising on first failure<br> <li> Wrap vars.h5 and obs.duckdb uploads in independent try/except blocks <br>to allow partial success<br> <li> Log warnings for individual artifact failures instead of raising <br>immediately<br> <li> Update <code>run</code> method to handle partial uploads: only include successfully <br>uploaded artifacts in payload<br> <li> Surface artifact errors only when <code>require_artifacts=True</code>, otherwise <br>continue with warning<br> <li> Add print statements for visual separation between artifact and job <br>submission phases</ul>

</details>

  </td>
  <td><a href="">+73/-52</a>&nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Tests</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>test_cytetype_integration.py</strong><dd><code>Update test for partial artifact uploads</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

tests/test_cytetype_integration.py

<ul><li>Update test docstring to reflect partial upload behavior<br> <li> Change assertion to expect <code>obs_duckdb</code> in payload when vars.h5 fails <br>but obs.duckdb succeeds<br> <li> Document that vars.h5 save fails independently while obs.duckdb still <br>succeeds</ul>

</details>

  </td>
  <td><a href="">+6/-3</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr></tbody></table>

</details>

___

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bee38ca8f1bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.