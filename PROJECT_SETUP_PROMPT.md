# PROJECT SETUP

## Role

Act as a **Senior Python Backend Engineer and DevOps-minded Project Maintainer**.

You are setting up a clean Python project from scratch in the current empty project folder.

Your goal is to create a professional, production-ready Python baseline with:

* Python virtual environment
* Git repository
* `.gitignore`
* `requirements.txt`
* `pyproject.toml`
* Ruff for formatting, import sorting, linting, security checks, complexity checks, and code-quality rules
* Mypy for strict static typing
* Pytest for testing
* Pytest coverage enforcement
* Pre-commit hooks
* Minimal source package structure
* Initial passing test suite
* Initial Git commit

Keep the setup clean, modern, strict, and maintainable.

---

## Context

This is a new Python project starting from an empty folder.

The project should use:

* Python virtual environment: `.venv`
* Git for version control
* `requirements.txt` for dependency installation
* `pyproject.toml` as the central tool configuration file
* `ruff` instead of Black, Isort, Flake8, and Bandit
* `mypy` for static typing
* `pytest` for testing
* `pytest-cov` / `coverage` for test coverage
* `pre-commit` for automated checks before commits

Do not add application frameworks yet.

Do not add FastAPI, Django, Flask, SQLAlchemy, pandas, NumPy, or trading-specific packages unless explicitly requested.

---

## Important Python Version Rule

Use the currently installed local Python version as the source of truth.

The base project configuration currently targets:

```toml
requires-python = ">=3.14"
python_version = "3.14"
```

However, Ruff currently uses:

```toml
target-version = "py313"
```

Before finalizing `pyproject.toml`, check the actual Python interpreter version.

Then do one of the following:

1. If the local Python version is Python 3.14 or newer:

   * Keep `requires-python = ">=3.14"`
   * Keep `mypy.python_version = "3.14"`
   * If Ruff supports `py314`, use `target-version = "py314"`
   * If Ruff does not support `py314`, use the highest supported Ruff target version and document the assumption.

2. If the local Python version is Python 3.13:

   * Change `requires-python = ">=3.13"`
   * Set `target-version = "py313"`
   * Set `mypy.python_version = "3.13"`

3. If the local Python version is lower than Python 3.13:

   * Stop and report that the project requires Python 3.13+.
   * Do not continue setup with an older Python version.

Do not leave mismatched Python versions in `pyproject.toml`.

---

## Task

Set up the project fully in the current directory.

Perform the following steps in order:

1. Check the installed Python version.
2. Create a Python virtual environment named `.venv`.
3. Use the `.venv` Python interpreter for all commands.
4. Upgrade `pip`.
5. Initialize a Git repository if one does not already exist.
6. Create a professional `.gitignore`.
7. Create the required project structure.
8. Create `requirements.txt` with the initial development packages.
9. Install all packages from `requirements.txt`.
10. Create and configure `pyproject.toml` using the Ruff-first configuration provided below.
11. Configure Ruff formatting.
12. Configure Ruff linting.
13. Configure Ruff import sorting.
14. Configure Ruff security checks.
15. Configure Ruff complexity rules.
16. Configure Mypy strict typing.
17. Configure Pytest.
18. Configure coverage so that:

    * Overall project coverage must be at least `80%`.
    * Coverage failures must fail the test command.
    * Each source file should target at least `80%` coverage by test discipline.
19. Configure Pre-commit.
20. Install Pre-commit hooks.
21. Create a simple source file and matching test file to verify the setup.
22. Run all quality checks.
23. Fix any issues found by the quality checks.
24. Run the final full validation suite.
25. Create the initial Git commit with the message:

```bash
chore: initial project setup
```

---

## Required Initial Project Structure

Create this structure:

```text
.
├── .gitignore
├── .pre-commit-config.yaml
├── pyproject.toml
├── requirements.txt
├── README.md
├── src/
│   └── app/
│       ├── __init__.py
│       └── main.py
└── tests/
    ├── __init__.py
    └── test_main.py
```

Use `src/app` as the default package for now.

Do not create unnecessary folders yet.

---

## Required Initial Packages

Create `requirements.txt` with:

```txt
ruff
mypy
pytest
pytest-cov
coverage
pre-commit
```

Do not include:

```txt
black
isort
flake8
bandit
```

Ruff replaces those tools.

You may add small, standard developer-quality packages only if they clearly improve the baseline setup.

Do not add application frameworks or business-domain packages.

---

## `.gitignore` Requirements

Create `.gitignore` with:

```gitignore
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python

# Virtual environments
.venv/
venv/
env/
ENV/

# Distribution / packaging
build/
dist/
*.egg-info/

# Test / coverage
.pytest_cache/
.coverage
coverage.xml
htmlcov/

# Type checking
.mypy_cache/
.dmypy.json
dmypy.json

# Ruff
.ruff_cache/

# IDEs / editors
.vscode/
.idea/

# OS files
.DS_Store
Thumbs.db

# Environment variables
.env
.env.*
!.env.example
```

---

## Required `pyproject.toml`

Use this as the base configuration.

Important:

* Reconcile the Python version before writing the final file.
* Do not leave `requires-python`, `tool.ruff.target-version`, and `tool.mypy.python_version` inconsistent.
* Keep Ruff as the only formatter, import sorter, linter, and security checker.
* Keep Mypy for typing.
* Keep Pytest and Coverage for tests.

```toml
[project]
name = "app"
version = "0.1.0"
description = "Initial Python project setup"
requires-python = ">=3.14"

[tool.ruff]
target-version = "py313"
line-length = 88
src = ["src", "tests"]

[tool.ruff.format]
quote-style = "double"
indent-style = "space"
line-ending = "auto"
docstring-code-format = true
docstring-code-line-length = 88

[tool.ruff.lint]
select = [
    "F",
    "E",
    "W",
    "C90",
    "I",
    "N",
    "D",
    "UP",
    "YTT",
    "ASYNC",
    "S",
    "BLE",
    "FBT",
    "B",
    "A",
    "COM",
    "C4",
    "DTZ",
    "T10",
    "DJ",
    "EM",
    "EXE",
    "FA",
    "ISC",
    "ICN",
    "LOG",
    "G",
    "INP",
    "PIE",
    "PYI",
    "PT",
    "Q",
    "RSE",
    "RET",
    "SLF",
    "SLOT",
    "SIM",
    "TID",
    "TC",
    "INT",
    "ARG",
    "PTH",
    "TD",
    "FIX",
    "PD",
    "PGH",
    "PL",
    "TRY",
    "FLY",
    "NPY",
    "FAST",
    "AIR",
    "PERF",
    "FURB",
    "RUF",
    "ANN",
]

ignore = [
    "FBT003",
    "D203",
    "D212",
    "D400",
    "D401",
    "D415",
    "S311",
    "PERF401",
    "RET504",
    "FA102",
    "TRY003",
    "EM101",
    "TC002",
    "TC003",
    "COM812",
    "ISC001",
]

[tool.ruff.lint.per-file-ignores]
"test_*.py" = ["S101", "S105", "S106", "S107", "PLR2004", "SLF001", "D", "ARG001", "PLC0415", "EM102", "ANN"]
"*_test.py" = ["S101", "S105", "S106", "S107", "PLR2004", "SLF001", "D", "ARG001", "PLC0415", "EM102", "ANN"]
"tests/**/*.py" = ["S101", "S105", "S106", "S107", "PLR2004", "SLF001", "D", "ARG001", "PLC0415", "EM102", "ANN"]
"conftest.py" = ["S101", "S105", "S106", "S107", "PLR2004", "SLF001", "D", "ARG001", "PLC0415", "EM102", "ANN"]

[tool.ruff.lint.mccabe]
max-complexity = 10

[tool.ruff.lint.pydocstyle]
convention = "google"

[tool.pytest.ini_options]
minversion = "7.0"
testpaths = ["tests"]
pythonpath = ["src"]
addopts = [
    "-ra",
    "--strict-markers",
    "--strict-config",
    "--cov=src/app",
    "--cov-report=term-missing",
    "--cov-report=html",
    "--cov-fail-under=80"
]

[tool.coverage.run]
branch = true
source = ["src/app"]

[tool.coverage.report]
show_missing = true
skip_covered = false
fail_under = 80
exclude_lines = [
    "pragma: no cover",
    "if TYPE_CHECKING:",
    "if __name__ == .__main__.:"
]

[tool.mypy]
python_version = "3.14"
strict = true
mypy_path = "src"
packages = ["app"]
warn_unused_configs = true
warn_return_any = true
warn_unused_ignores = true
warn_redundant_casts = true
disallow_untyped_defs = true
disallow_incomplete_defs = true
check_untyped_defs = true
no_implicit_optional = true
```

---

## Pre-commit Requirements

Create `.pre-commit-config.yaml`.

Use Pre-commit hooks for:

* trailing whitespace cleanup
* end-of-file fixer
* YAML checks
* TOML checks
* large file checks
* Ruff check with auto-fix
* Ruff format
* Mypy

Example baseline:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v5.0.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-toml
      - id: check-added-large-files

  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.8.0
    hooks:
      - id: ruff
        args: ["--fix"]
      - id: ruff-format

  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.13.0
    hooks:
      - id: mypy
        additional_dependencies: []
```

If newer stable compatible versions are available, use newer versions.

Do not add Black, Isort, Flake8, or Bandit pre-commit hooks.

---

## Initial Source File

Create `src/app/main.py`:

```python
"""Application entry module."""


def add_numbers(first: int, second: int) -> int:
    """Return the sum of two integers."""
    return first + second
```

---

## Initial Test File

Create `tests/test_main.py`:

```python
"""Tests for the application entry module."""

from app.main import add_numbers


def test_add_numbers_returns_sum() -> None:
    """Return sum when two integers are provided."""
    assert add_numbers(2, 3) == 5
```

---

## README Requirements

Create `README.md` with:

````md
# App

Initial Python project setup.

## Setup

Create the virtual environment:

```bash
python -m venv .venv
```

Activate the environment:

### Windows PowerShell

```bash
.venv\Scripts\Activate.ps1
```

### macOS / Linux

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Install pre-commit hooks:

```bash
pre-commit install
```

Run checks:

```bash
ruff format --check src tests
ruff check src tests
mypy src
pytest
pre-commit run --all-files
```
````

Ensure Markdown formatting is valid.

---

## Commands to Run

Run the equivalent of these commands, adjusting for the operating system and shell.

Use the `.venv` Python interpreter.

### Windows PowerShell

```powershell
py -3 -m venv .venv
.\.venv\Scripts\python -m pip install --upgrade pip
.\.venv\Scripts\python -m pip install -r requirements.txt

git init

.\.venv\Scripts\pre-commit install

.\.venv\Scripts\ruff format src tests
.\.venv\Scripts\ruff check src tests --fix
.\.venv\Scripts\mypy src
.\.venv\Scripts\pytest

.\.venv\Scripts\pre-commit run --all-files

git add .
git commit -m "chore: initial project setup"
```

### macOS / Linux

```bash
python -m venv .venv
.venv/bin/python -m pip install --upgrade pip
.venv/bin/python -m pip install -r requirements.txt

git init

.venv/bin/pre-commit install

.venv/bin/ruff format src tests
.venv/bin/ruff check src tests --fix
.venv/bin/mypy src
.venv/bin/pytest

.venv/bin/pre-commit run --all-files

git add .
git commit -m "chore: initial project setup"
```

Important:

* Do not rely on globally installed packages.
* Use `.venv` executables directly.
* If `pre-commit run --all-files` modifies files, stage the changes and re-run it.
* Only commit after all checks pass.

---

## Required Quality Gates

The setup is only complete when all of these pass:

```bash
ruff format --check src tests
ruff check src tests
mypy src
pytest
pre-commit run --all-files
```

Coverage must be at least `80%`.

If any check fails:

1. Read the error.
2. Fix the root cause.
3. Re-run the failed command.
4. Re-run all quality gates before committing.

---

## Coverage Requirements

Configure coverage so that:

* `pytest` fails if total coverage is below `80%`.
* The terminal report shows missing lines.
* HTML coverage is generated in `htmlcov/`.
* Branch coverage is enabled.

Target discipline:

* Every production source file should have matching tests.
* Every production source file should target at least `80%` meaningful test coverage.
* Do not game coverage with meaningless tests.
* Do not exclude real logic from coverage without a clear reason.

---

## Constraints

Do not:

* Add Black.
* Add Isort.
* Add Flake8.
* Add Bandit.
* Add unnecessary frameworks.
* Add unnecessary folders.
* Skip coverage.
* Skip Mypy.
* Skip Pre-commit.
* Commit if checks are failing.
* Leave Python version settings inconsistent.
* Use global Python packages when `.venv` exists.
* Add secrets or local `.env` files to Git.

Do:

* Use Ruff for formatting.
* Use Ruff for import sorting.
* Use Ruff for linting.
* Use Ruff for security checks.
* Use Ruff for complexity checks.
* Use Mypy for strict static typing.
* Use Pytest for tests.
* Keep the project minimal.
* Keep configuration centralized in `pyproject.toml`.
* Make the project immediately usable.

---

## Final Validation

Before committing, run:

```bash
ruff format --check src tests
ruff check src tests
mypy src
pytest
pre-commit run --all-files
```

If all pass, commit:

```bash
git add .
git commit -m "chore: initial project setup"
```

---

## Final Response Required

After completing the setup, return a concise summary with:

1. Python version used.
2. Files created.
3. Packages installed.
4. Quality commands successfully run.
5. Coverage result.
6. Git commit hash.
7. Any assumptions made.

Do not include unnecessary explanation.
