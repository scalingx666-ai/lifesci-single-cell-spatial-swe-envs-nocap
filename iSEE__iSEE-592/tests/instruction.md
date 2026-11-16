# Issue

**Title:** Bugfix setting the active multi-selection info of Table panels

## Description

Table panels are not re-rendered when their search boxes are used to filter them (otherwise, it would create that annoying effect of the cursor losing the focus from the search box are each character typed because the cursor does not refocus on the search box after the panel is re-rendered).

This means that the info message indicating the number and fraction of rows selected is out-of-date most of the time (it is only updated if the table panel is re-rendered due to an incoming selection forcing the table panel to re-render due to repopulation of the table.

This fix... fixes the content of the ui info for Table panels to a message that redirects users to the `DT::datatable` built-in message that already reports that information.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ffebe8179296`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.