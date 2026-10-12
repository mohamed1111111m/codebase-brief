# Publishing Codebase Brief to PyPI

The package is configured as `codebase-brief` version `0.1.0`. Publishing is automated through GitHub Actions Trusted Publishing; no PyPI API token is stored in this repository.

## One-time account setup

1. Create or sign in to your personal account at [PyPI](https://pypi.org/account/register/).
2. On PyPI, add a pending Trusted Publisher for the first upload:
   - Owner: `mohamed1111111m`
   - Repository: `codebase-brief`
   - Workflow: `publish.yml`
   - Environment: `pypi`
3. In GitHub, open **Settings → Environments** and create an environment named `pypi`. Consider requiring approval before a release workflow publishes.
4. Confirm the project version and release notes in `pyproject.toml` and `CHANGELOG.md`.
5. Create a GitHub Release with tag `v0.1.0`. Publishing the release triggers `.github/workflows/publish.yml` to build, validate, and upload the package.

The first successful upload claims the `codebase-brief` name on PyPI. Check the PyPI project page first to ensure another publisher has not claimed it since the last availability check. PyPI releases are immutable; use a new version number for corrections.

## Verify after publication

Wait for the [PyPI project page](https://pypi.org/project/codebase-brief/) to appear, then use a clean virtual environment:

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
