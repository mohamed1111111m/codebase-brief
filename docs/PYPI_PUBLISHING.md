# Publishing Codebase Brief to PyPI

The package is configured as `codebase-brief`. Publishing is automated through GitHub Actions Trusted Publishing; no PyPI API token is stored in this repository. PyPI releases are immutable, so every release needs a new version in `pyproject.toml` and the app's `VERSION` constant.

## Current publisher setup

The package already exists on PyPI. Its GitHub Trusted Publisher is configured for owner `mohamed1111111m`, repository `codebase-brief`, workflow `publish.yml`, and GitHub environment `pypi`. Do not create a second publisher for routine releases.

For each release:

1. Update the version in `pyproject.toml` and `context_inject/cli.py`.
2. Move completed changes into a versioned section in `CHANGELOG.md` and check the README install instructions.
3. Run the local release checks below.
4. Push the release commit to `main`, then create a GitHub Release with a matching tag such as `v0.1.2`. Publishing the GitHub Release triggers `.github/workflows/publish.yml` to build, validate, and upload the package.
5. Check the Actions run and the [PyPI project page](https://pypi.org/project/codebase-brief/) to confirm the upload.

PyPI releases are immutable; use a new version number for corrections.

## Verify after publication

After the new version appears on the [PyPI project page](https://pypi.org/project/codebase-brief/), verify it in a clean virtual environment:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade codebase-brief
codebase-brief --help
```

On macOS or Linux, create the environment with `python3 -m venv .venv` and activate it with `source .venv/bin/activate`.

## Local release checks

From the repository root:

```powershell
python -m build
python -m twine check dist/*
```

The GitHub workflow repeats these checks before it publishes.
