# PROJECT SETUP

## Role

Act as a **Senior Python Backend Engineer and DevOps-minded Project Maintainer**.

You are setting up a clean Python project from scratch in the current empty project folder.

Your goal is to create a professional, production-ready baseline with:

* Virtual environment
* Git repository
* Dependency management
* Code formatting
* Linting
* Static typing
* Testing
* Coverage enforcement
* Pre-commit hooks
* Sensible project structure
* Initial commit

Do not over-engineer the setup. Keep it clean, practical, and maintainable.

---

## Context

This is a new Python project starting from an empty folder.

The project should use:

* Python virtual environment: `.venv`
* Git for version control
* `requirements.txt` for dependencies
* `pyproject.toml` for tool configuration
* `pytest` for testing
* `coverage.py` / `pytest-cov` for coverage
* `black` for formatting
* `isort` for import sorting
* `flake8` for linting
* `mypy` for static typing
* `pre-commit` for automated checks before commits

The setup should be compatible with a normal Python project and should not assume a specific application framework yet.

---

## Task

Set up the project fully in the current directory.

Perform the following steps in order:

1. Create a Python virtual environment named `.venv`.
2. Activate/use the virtual environment for all Python and pip commands.
3. Initialize a Git repository if one does not already exist.
4. Create a professional `.gitignore`.
5. Create a minimal but useful Python package structure.
6. Create `requirements.txt` with initial development packages.
7. Install all packages from `requirements.txt`.
8. Create and configure `pyproject.toml`.
9. Configure formatting with `black`.
10. Configure import sorting with `isort`.
11. Configure type checking with `mypy`.
12. Configure test settings with `pytest`.
13. Configure test coverage so that:

    * Overall project coverage must be at least `80%`.
    * Each tested source file should target at least `80%` coverage.
    * Coverage failures should fail the test command.
14. Configure `flake8`.
15. Configure `pre-commit`.
16. Install pre-commit hooks.
17. Create a simple source file and matching test file to verify the setup.
18. Run all quality checks.
19. Fix any issues found by the quality checks.
20. Create the initial Git commit with the message:

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

Create `requirements.txt` with at least:

```txt
black
isort
flake8
mypy
pytest
pytest-cov
coverage
pre-commit
```

You may add small, standard developer-quality packages only if they clearly improve the baseline setup.

Do not add application frameworks such as FastAPI, Django, Flask, SQLAlchemy, or pandas unless explicitly requested.

---

## `.gitignore` Requirements

Create a `.gitignore` that covers:

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

# Linters / formatters
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

## `pyproject.toml` Requirements

Create and update `pyproject.toml` with configuration for:

* Project metadata
* `black`
* `isort`
* `pytest`
* `coverage`
* `mypy`

Use these standards unless there is a strong reason not to:

```toml
[project]
name = "app"
version = "0.1.0"
description = "Initial Python project setup"
requires-python = ">=3.11"

[tool.black]
line-length = 88
target-version = ["py311"]

[tool.isort]
profile = "black"
line_length = 88
src_paths = ["src", "tests"]

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
python_version = "3.11"
strict = true
mypy_path = "src"
packages = ["app"]
warn_unused_configs = true
warn_return_any = true
warn_unused_ignores = true
disallow_untyped_defs = true
disallow_incomplete_defs = true
check_untyped_defs = true
no_implicit_optional = true
```

If the installed Python version is not Python 3.11, adjust the `requires-python`, `target-version`, and `python_version` fields to match the actual local version.

---

## `flake8` Configuration

Because `flake8` does not natively read `pyproject.toml`, create a `.flake8` file with:

```ini
[flake8]
max-line-length = 88
extend-ignore = E203,W503
exclude =
    .git,
    .venv,
    __pycache__,
    build,
    dist,
    .mypy_cache,
    .pytest_cache
```

---

## `pre-commit` Requirements

Create `.pre-commit-config.yaml` with hooks for:

* trailing whitespace cleanup
* end-of-file fixer
* YAML checks
* TOML checks
* large file checks
* black
* isort
* flake8
* mypy

Use stable official repos where possible.

Example baseline:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.6.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-toml
      - id: check-added-large-files

  - repo: https://github.com/psf/black
    rev: 24.8.0
    hooks:
      - id: black

  - repo: https://github.com/PyCQA/isort
    rev: 5.13.2
    hooks:
      - id: isort

  - repo: https://github.com/PyCQA/flake8
    rev: 7.1.1
    hooks:
      - id: flake8

  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.11.2
    hooks:
      - id: mypy
        additional_dependencies: []
```

If newer compatible versions are available in the environment, using newer stable versions is acceptable.

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
    """It returns the sum of two integers."""
    assert add_numbers(2, 3) == 5
```

---

## README Requirements

Create a simple `README.md` with:

````md
# App

Initial Python project setup.

## Setup

```bash
python -m venv .venv
````

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
black --check src tests
isort --check-only src tests
flake8 src tests
mypy src
pytest
```

````

Ensure the Markdown formatting is valid.

---

## Commands to Run

Run the equivalent of these commands, adjusting for the operating system and shell:

```bash
python -m venv .venv
python -m pip install --upgrade pip
python -m pip install -r requirements.txt

git init

pre-commit install

black src tests
isort src tests
flake8 src tests
mypy src
pytest

pre-commit run --all-files

git add .
git commit -m "chore: initial project setup"
````

Important:

* Use the `.venv` Python interpreter when installing and running tools.
* On Windows, use `.venv\Scripts\python`.
* On macOS/Linux, use `.venv/bin/python`.
* Do not rely on globally installed packages.

---

## Quality Gates

The setup is only complete when all of these pass:

```bash
black --check src tests
isort --check-only src tests
flake8 src tests
mypy src
pytest
pre-commit run --all-files
```

Testing must enforce at least `80%` coverage.

If any check fails:

1. Read the error.
2. Fix the root cause.
3. Re-run the failed command.
4. Re-run all quality gates before committing.

---

## Constraints

Do not:

* Add unnecessary frameworks.
* Add unnecessary folders.
* Skip test coverage configuration.
* Skip pre-commit setup.
* Commit broken checks.
* Ignore linting or typing failures.
* Use global Python packages when `.venv` exists.
* Create placeholder files that serve no purpose.
* Add secrets or local environment files to Git.

Do:

* Keep the setup minimal.
* Keep configuration centralized in `pyproject.toml` where supported.
* Use `.flake8` only because flake8 does not natively support `pyproject.toml`.
* Make the project immediately usable.
* Ensure the initial commit only happens after all checks pass.

---

## Final Response Required

After completing the setup, return a concise summary with:

1. Files created.
2. Packages installed.
3. Commands successfully run.
4. Coverage result.
5. Git commit hash for the initial setup commit.
6. Any assumptions made.

Do not include unnecessary explanation.
