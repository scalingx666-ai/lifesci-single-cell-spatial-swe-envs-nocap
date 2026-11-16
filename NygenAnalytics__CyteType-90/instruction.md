# Issue

**Title:** Add CLI authentication and automatic SDK credential loading

## Description

## Summary

This PR adds a packaged `cytetype` command-line interface and connects it to the existing Python SDK.

Users can authenticate once through their browser with `cytetype setup`. The resulting API key is stored in an owner-only local credential file and automatically used by subsequent SDK annotation and upload requests.

Users can also save an existing API key using `cytetype login`.

## CLI commands

- `cytetype setup`
  - Starts a PKCE browser authorization flow.
  - Opens the configured CyteType login page.
  - Prints the authorization URL when the browser cannot be opened.
  - Receives the authorization result through a local callback.
  - Saves the returned credentials.
  - Shows a branded success page and redirects to the dashboard after five seconds.

- `cytetype get-key`
  - Alias for `cytetype setup`.

- `cytetype login`
  - Prompts for an existing API key using hidden terminal input.
  - Validates the key with the server.
  - Retrieves and stores the associated user metadata.

- `cytetype dashboard`
  - Prints and opens the dashboard associated with the saved server.

- `cytetype view JOB_ID`
  - Prints and opens the web report for a job.
  - Does not place the API key in the URL.

- `cytetype logout`
  - Deletes local credentials.
  - Does not revoke the server-side API key.

- `cytetype --version`
  - Prints the installed CyteType version.

## Credential storage

Credentials are stored in:

- `$XDG_CONFIG_HOME/cytetype/credentials.json` when configured.
- `%APPDATA%/cytetype/credentials.json` on Windows.
- `~/.config/cytetype/credentials.json` by default.

The credential file contains:

- API URL
- Dashboard URL
- API key
- Token ID
- User ID
- Email

Storage behavior:

- Parent directory is restricted to the current user.
- Credential file mode is set to `0600`.
- Writes use a temporary file followed by an atomic replacement.
- Credentials are bound to their saved API URL.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b11b5d3d5cb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.