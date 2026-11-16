# Issue

**Title:** Support parallel chunked uploads and bump version

## Description

### **User description**
Bump package version to 0.16.0 and add support for chunked, parallel file uploads. Introduces a chunked upload flow (initiate -> parallel PUT of chunks -> complete) with server-side size checks and an adjustable max_workers parameter (default 4). HTTPTransport gained post_empty() for no-body POSTs and put_binary() to upload raw binary via PUT. Client upload helpers (upload_obs_duckdb, upload_vars_h5) and CyteType entry points now accept/upload_max_workers and pass it through. Parallel uploads use ThreadPoolExecutor and per-thread HTTPTransport (threading.local) to keep memory bounded (~max_workers × chunk_size) and maintain connection safety. The final complete response is parsed into the existing UploadResponse shape.

___

### **PR Type**
Enhancement

___

### **Description**
- Implement parallel chunked file uploads with configurable worker threads

- Add `post_empty()` and `put_binary()` methods to HTTPTransport for new upload flow

- Introduce three-step upload process: initiate, parallel chunk upload, complete

- Add `upload_max_workers` parameter (default 4) to upload functions and CyteType.run()

- Bump version to 0.16.0

___

### File Walkthrough

<table><thead><tr><th></th><th align="left">Relevant files</th></tr></thead><tbody><tr><td><strong>Configuration changes</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>__init__.py</strong><dd><code>Version bump to 0.16.0</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/__init__.py

- Bump package version from 0.15.0 to 0.16.0

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Enhancement</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>client.py</strong><dd><code>Implement parallel chunked upload flow</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/api/client.py

<ul><li>Add imports for <code>math</code>, <code>threading</code>, and <code>ThreadPoolExecutor</code> to support <br>parallel uploads<br> <li> Refactor <code>_upload_file()</code> to implement three-step chunked upload flow: <br>initiate, parallel chunk upload via ThreadPoolExecutor, complete<br> <li> Add <code>max_workers</code> parameter (default 4) to <code>_upload_file()</code>, <br><code>upload_obs_duckdb()</code>, and <code>upload_vars_h5()</code><br> <li> Use thread-local storage for per-thread HTTPTransport instances to <br>maintain connection safety and bound memory usage</ul>

</details>

  </td>
  <td><a href="">+66/-9</a>&nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>transport.py</strong><dd><code>Add post_empty and rename post_binary to put_binary</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/api/transport.py

<ul><li>Add <code>post_empty()</code> method to make POST requests with no body for upload <br>initiation and completion<br> <li> Rename <code>post_binary()</code> to <code>put_binary()</code> and change HTTP method from POST <br>to PUT for chunk uploads<br> <li> Update docstring to reflect PUT method usage</ul>

</details>

  </td>
  <td><a href="">+27/-3</a>&nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>main.py</strong><dd><code>Add upload_max_workers parameter to CyteType.run()</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/main.py

<ul><li>Add <code>upload_max_workers</code> parameter (default 4) to <br><code>_build_and_upload_artifacts()</code> method<br> <li> Add <code>upload_max_workers</code> parameter (default 4) to <code>run()</code> method with <br>documentation<br> <li> Pass <code>upload_max_workers</code> through to <code>upload_obs_duckdb_file()</code> and <br><code>upload_vars_h5_file()</code> calls<br> <li> Update docstring to document the new parameter and its memory <br>implications</ul>

</details>

  </td>
  <td><a href="">+7/-0</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr></tbody></table>

___

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fdf94c2765e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.