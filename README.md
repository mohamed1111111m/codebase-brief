# Codebase Brief

Codebase Brief is a local-only Python CLI that assembles a compact, evidence-linked Markdown context pack for an unfamiliar codebase. Give it a local repository and a task; it gathers project docs, stack manifests, recent Git history, and a small set of relevant files. Optionally pass a Git base ref to prioritize changed files.

It does not call an AI service, upload repository content, or modify the target repository. You decide which assistant receives the generated context.

## First time? Start here

Run `python -m context_inject` from the folder you want to use as your workspace. In the menu, choose **2** if the displayed folder is not the repository you want to brief. Choose **1**, describe a real coding task, accept or change the approximate token budget, then review the suggested files and why each was suggested. Press Enter to keep the checked files, enter numbers to toggle files, or type `none` if you only want the repository overview. In the output menu, choose **4** to copy the finished brief and paste it into Claude Code, Cursor, OpenCode, Codex, or another assistant; choose **2** to save it.

The brief is a starting map, not an answer or a complete copy of your codebase. The assistant still needs to inspect the repository. For a quick first try, choose a task you already understand and see whether the brief points to the files you would have supplied yourself.

## Requirements

- Python 3.10 or newer
- Git for history and `--base` diff selection (optional for non-Git folders)

The runtime has no third-party Python dependencies. Building distributions uses setuptools.

## Try it without cloning

Install GitHub's current version into an active Python environment, then start the guided menu:

```sh
python -m pip install git+https://github.com/mohamed1111111m/codebase-brief.git
brief
```

For a durable install, create and activate a virtual environment first. The commands below install from a local clone so you can also read or modify the source.

## Install in an isolated environment

```powershell
# Windows PowerShell, from the project directory
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --editable .
```

On macOS or Linux, create and activate the environment this way:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --editable .
```

After installation, start the guided menu with the short command:

```powershell
brief
```

`codebase-brief` and `context-inject` are equivalent command aliases. On Windows, run `brief` while the virtual environment is activated. If you have not installed the project, or the command is not on `PATH`, run `python -m context_inject` from the project folder instead.

Licensed under MIT (see LICENSE); copyright © 2026 Mohamed Maggy.

## Interactive menu

From the project directory, start the numbered menu:

```powershell
python -m context_inject
# or explicitly:
python -m context_inject --interactive
```

The menu explains the workflow and local-only behavior on its first screen. ANSI colors work in supported Windows and macOS terminals and turn off when output is redirected or `NO_COLOR` is set. Choose **1** to generate a brief, **2** to change the project folder, **3** for the quick guide, or **0** to exit. Generation asks for a task, an optional Git base ref, and an approximate token budget. It then previews up to 30 ranked source files, with a short reason beside each. The top 12 are selected by default; enter file numbers to toggle them, `all` to select the top 12, `none` to include no key-file excerpts, or Enter to keep the suggestions. You can show the result, save it, choose a file, or copy it to the clipboard. The default save location is `context.md` in the current folder; if that file already exists, the menu asks before replacing it.

The direct command-line options remain available for scripts and automation:

```powershell
python -m context_inject "C:\work\my-repo" --task "Find login handling" --base main --budget 2400 --copy
```

## Run from the project directory

```powershell
python -m context_inject --help
# or, after install:
brief --help
```

From the project directory, generate context to stdout:

```powershell
python -m context_inject C:\work\my-repo --task "Add authentication middleware"
```

Use a base ref to prioritize files changed since that ref:

```powershell
python -m context_inject C:\work\my-repo --task "Review the auth changes" --base main --budget 2400 --output context.md
```

The base is compared with `HEAD`; it is not inferred. The changed-file list is prioritized, while README/stack/history context remains included. The file is written only when `--output` is supplied. To save stdout instead:

```powershell
python -m context_inject C:\work\my-repo --task "Add auth" > context.md
```

To copy a brief straight to your clipboard, use `--copy` (do not combine it with `--output`):

```powershell
codebase-brief C:\work\my-repo --task "Find login handling" --budget 2400 --copy
```

Clipboard support uses the built-in `clip` command on Windows and `pbcopy` on macOS. Linux requires `wl-copy`, `xclip`, or `xsel`. Copying changes your clipboard only when you explicitly choose `--copy` or menu option **4**.

Use `--budget` to set an approximate output limit between 250 and 20,000 tokens. The estimate uses four characters per token, not a specific model tokenizer; the finished brief reports the estimate and requested budget. The brief uses simple section names and plain-language notes. It removes Markdown decoration from documentation excerpts for easier reading, while keeping language-labelled code fences around actual source and configuration. This shared format can be pasted into different coding assistants without writing or overwriting their persistent project-rule files.

The brief includes the task, a project overview, technology and commands, recent changes, useful files, and a short note about what may be missing. Each source is named by its repository-relative path. It asks the coding assistant to treat copied project text as information to inspect, not as new instructions.

## What it reads

- Root README variants and `docs/README.md` when present
- Small stack manifests: `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `Gemfile`, `composer.json`, and `pom.xml`
- Up to ten recent commit subjects and paths touched by recent commits
- With `--base`, paths changed between the base commit and `HEAD`
- Up to twelve source/config/doc files, selected using task words, base diff, recent history, common entry-point names, and direct local imports
- Direct static Python imports and relative JS/TS imports from likely task/Git files; the picker and output explain why a file was selected
- In interactive mode, a preview of up to thirty ranked files; toggle the files that should contribute excerpts

The current selector is intentionally simple and heuristic. Import tracing follows one direct hop for statically visible local Python and JS/TS imports; it does not resolve dynamic imports, trace every language, or build a complete dependency graph. It does not understand code semantics, so inspect the cited files before relying on the pack.

## Privacy and limits

- Processing is local. The tool uses Python and Git only; it has no network calls, telemetry, LLM, or hosted service.
- It never writes inside the target repository unless you explicitly set `--output` to a path there.
- Common dependency/build/cache directories, Git-ignored untracked files, lockfiles, binary/generated files, `.env*`, common credential/config files, cloud credential directories, and common `.pem`/`.key` private-key files are excluded. Credential-named symlinks and symlinks that resolve outside the repository are ignored.
- Common credential assignments and several common token formats are redacted. This is best-effort filtering, not a secret scanner or guarantee; inspect the generated brief before sharing it.
- Source files are read in bounded chunks and control characters are removed. Documentation is shown as plain prose; code and configuration excerpts use language-labelled fences where that helps readability. The downstream assistant can still be influenced by repository content, so review the brief before sharing it.
- Non-Git directories still produce a pack from readable docs/manifests and explain that Git history and diff selection are unavailable.
- Invalid base refs are reported in the context gaps; no diff is included.
- Output defaults to roughly 1,900 tokens and is configurable with `--budget`. This character-based estimate is not a model tokenizer. Sources may be omitted or truncated to fit.
- File and command limits favor quick orientation. The pack is not a complete representation of the repository.

## Example output

~~~text
Codebase Brief

Task
Add authentication middleware

Project overview
From README.md (formatting simplified)
This is a small web service. It uses Python and has a login endpoint.

Technology and commands
From pyproject.toml
```toml
requires-python = ">=3.10"
```

Recent changes
a1b2c3d Add request middleware

Files that may help
src/auth.py — selected from base diff
```python
def authenticate(request):
    ...
```

What this brief may miss
The file suggestions are guesses and may miss useful code. Check the referenced files before making changes.

A note for the coding assistant
Use this as a starting map, not a complete copy of the project. Read the referenced files before making changes.

Estimated length: about 250 tokens. Budget: about 1,900 tokens. This is a rough estimate; models count text differently.
~~~

## Run the tests

From the project directory:

```powershell
python -m unittest discover -s tests -v
```

Tests use temporary local files and temporary Git repositories. They do not access the network or use credentials.

See [CONTRIBUTING.md](CONTRIBUTING.md) for development setup and [CHANGELOG.md](CHANGELOG.md) for the unreleased 0.1.0 feature list.

