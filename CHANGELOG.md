# Changelog

## Unreleased

- Add a clear instruction for the receiving assistant to answer the task using the brief as context.
- Prioritize task-relevant source excerpts ahead of stack details and Git history when the requested budget is small.
- Let users add a safe repository file by path and print a copyable summary of reviewed file selections.
- Print review feedback after the generated brief, and prioritize direct local importers of files changed since `--base`.
- Resolve literal Python dynamic imports and simple JS/TS path aliases when tracing imports.

## 0.1.0

- Generate bounded, local Markdown context briefs from project documentation, manifests, Git history, and selected source files.
- Add an interactive terminal menu with ranked file selection, output choices, and overwrite confirmation.
- Explain first-run usage in the menu and CLI help; show why each source file was selected.
- Follow one level of local Python and JavaScript/TypeScript imports; allow approximate token budgets and clipboard handoff to any coding assistant.
- Format generated briefs with plain-language section titles, readable documentation excerpts, and code fences only for source/configuration where useful.
- Exclude common credential files and Git-ignored untracked files, reject credential-named or external symlinks, redact common secret formats, and keep source excerpts within fixed limits.
- Preserve normal typed password parameters and conditions in source excerpts while redacting quoted credential assignments.
- Package the CLI as `codebase-brief`, retaining `context-inject` as a compatibility command.

