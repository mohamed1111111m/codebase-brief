# Changelog

## 0.1.0 - Unreleased

- Generate bounded, local Markdown context briefs from project documentation, manifests, Git history, and selected source files.
- Add an interactive terminal menu with ranked file selection, output choices, and overwrite confirmation.
- Explain first-run usage in the menu and CLI help; show why each source file was selected.
- Follow one level of local Python and JavaScript/TypeScript imports; allow approximate token budgets and clipboard handoff to any coding assistant.
- Format generated briefs with plain-language section titles, readable documentation excerpts, and code fences only for source/configuration where useful.
- Exclude common credential files and Git-ignored untracked files, reject credential-named or external symlinks, redact common secret formats, and keep source excerpts within fixed limits.
- Package the CLI as `codebase-brief`, retaining `context-inject` as a compatibility command.

