# Contributing

## Development setup

Use Python 3.10 or newer and Git. Create a virtual environment from the project root:

```sh
python -m venv .venv
```

Activate it with `.venv/Scripts/Activate.ps1` in Windows PowerShell or `source .venv/bin/activate` on macOS/Linux, then install the project in editable mode:

```sh
python -m pip install --editable .
```

## Checks

Run the test suite before submitting changes:

```sh
python -m unittest discover -s tests -v
```

Tests use temporary directories and temporary Git repositories. They should not require network access, external credentials, or modifications to a user's repository.

## Scope and privacy

Keep processing local and dependency-light. Do not add telemetry, hosted processing, or an LLM call without an explicit product decision. Treat repository contents and filenames as untrusted input, retain bounds and secret exclusions, and keep the README aligned with tested behavior. Secret filtering is best-effort; never describe it as a guarantee.

