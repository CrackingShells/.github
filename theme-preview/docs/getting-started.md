# Getting Started

This page tests **code blocks**, **tabbed content**, **inline code**, and **numbered steps** — all typical in documentation first-run guides.

---

## Installation

=== "pip"

    ```bash
    pip install hatch
    ```

=== "pipx (recommended)"

    ```bash
    pipx install hatch
    ```

=== "conda"

    ```bash
    conda install -c conda-forge hatch
    ```

Verify the installation:

```bash
hatch --version
# Hatch, version 1.x.y
```

---

## Quick Start

### 1. Create a new project

```bash
hatch new my-project
cd my-project
```

This scaffolds the following structure:

```
my-project/
├── src/
│   └── my_project/
│       ├── __init__.py
│       └── app.py
├── tests/
│   └── test_app.py
├── pyproject.toml
└── README.md
```

### 2. Add a dependency

Open `pyproject.toml` and add to `[project.dependencies]`:

```toml
[project]
name = "my-project"
version = "0.1.0"
dependencies = [
  "requests>=2.31",
  "rich>=13.0",
]
```

### 3. Enter the default environment

```bash
hatch shell
```

Hatch automatically creates a virtual environment the first time. Inside the shell you have access to all declared dependencies.

### 4. Run tests

```bash
hatch run test
```

Under the hood this calls:

```bash
pytest tests/ -v --tb=short
```

---

## Environment Matrix

You can define a matrix to test against multiple Python versions simultaneously:

```toml
[tool.hatch.envs.test.overrides]
matrix.python.python = ["3.10", "3.11", "3.12", "3.13"]
```

Run all matrix variants in parallel:

```bash
hatch run test:all
```

!!! tip "Speed tip"
    Use `hatch run +py=3.12 test` to target a single matrix cell without running all variants.

---

## Inline code examples

- Package identifier: `my-project`
- Config file: `pyproject.toml`
- Environment variable: `HATCH_ENV_ACTIVE`
- CLI flag: `--verbose` / `-v`

Keyboard shortcuts work too: press ++ctrl+c++ to abort a running command.

---

## Next steps

- Read the [Configuration](configuration.md) reference to learn all `pyproject.toml` options
- Explore the [API Reference](api-reference.md) for the Python programmatic interface
