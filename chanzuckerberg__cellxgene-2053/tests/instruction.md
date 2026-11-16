# Issue

**Title:** improve error message for OBO parse failure

## Description

The OBO file specified for use in the experimental ontology support may have syntax errors, causing parsing failure.  The error messages around this were opaque, leading to confusion about root cause of startup failures (see bug #2034).

The error messaging is now includes specific information about the source of the error, line number and offset, in standard parser error format (file:lineno:offset).

Example:
```
Error: Unable to load ontology terms
http://purl.obolibrary.org/obo/cl.obo:31344:12 OBO syntax error, unable to read ontology
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3aef21f76c5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.