# Configuration Reference

This page tests **long tables**, **many headings** (exercises `toc.follow`), and extended **YAML/TOML code blocks**.

---

## `pyproject.toml` Overview

All Hatch configuration lives in `pyproject.toml` under the `[tool.hatch]` namespace.

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my-project"
dynamic = ["version"]
description = "A concise description of my project."
readme = "README.md"
requires-python = ">=3.10"
license = "MIT"
keywords = ["python", "packaging"]
classifiers = [
  "Development Status :: 4 - Beta",
  "Programming Language :: Python :: 3",
]
dependencies = [
  "requests>=2.31",
]

[project.optional-dependencies]
dev  = ["pytest>=8", "coverage[toml]"]
docs = ["mkdocs>=1.6", "mkdocs-material>=9.5", "mkdocstrings[python]>=0.25"]
```

---

## Version Management

### Static versioning

```toml
[project]
version = "1.2.3"
```

### Dynamic versioning (VCS-based)

```toml
[project]
dynamic = ["version"]

[tool.hatch.version]
source = "vcs"
```

Requires `hatch-vcs` as a build dependency:

```toml
[build-system]
requires = ["hatchling", "hatch-vcs"]
```

### Version bumping

```bash
hatch version patch   # 1.2.3 → 1.2.4
hatch version minor   # 1.2.3 → 1.3.0
hatch version major   # 1.2.3 → 2.0.0
hatch version 2.0.0b1 # explicit pre-release
```

---

## Environments

### Default environment

```toml
[tool.hatch.envs.default]
dependencies = [
  "pytest>=8",
  "pytest-cov",
]

[tool.hatch.envs.default.scripts]
test    = "pytest {args:tests}"
test-cov = "pytest --cov=src {args:tests}"
```

### Named environments

```toml
[tool.hatch.envs.lint]
dependencies = ["ruff>=0.4", "mypy>=1.10"]

[tool.hatch.envs.lint.scripts]
check = ["ruff check src", "mypy src"]
fmt   = "ruff format src"
```

### Matrix environments

```toml
[[tool.hatch.envs.test.matrix]]
python = ["3.10", "3.11", "3.12", "3.13"]
```

---

## Build Targets

### Wheel

```toml
[tool.hatch.build.targets.wheel]
packages = ["src/my_project"]
```

### Source distribution

```toml
[tool.hatch.build.targets.sdist]
include = [
  "/src",
  "/tests",
  "LICENSE",
  "README.md",
]
exclude = [
  "*.pyc",
  "__pycache__",
  ".DS_Store",
]
```

---

## Build Hooks

Custom build hooks run during `hatch build`:

```toml
[tool.hatch.build.hooks.custom]
path = "hatch_build.py"
```

```python
# hatch_build.py
from hatchling.builders.hooks.plugin.interface import BuildHookInterface

class CustomBuildHook(BuildHookInterface):
    def initialize(self, version, build_data):
        # Runs before the build
        build_data["shared_data"]["generated"] = True
```

---

## All Configuration Keys

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| `tool.hatch.version.source` | `str` | `"regex"` | Version source (`regex`, `vcs`, `env`) |
| `tool.hatch.version.path` | `str` | — | Path to file containing version string |
| `tool.hatch.version.pattern` | `str` | see docs | Regex capturing named group `version` |
| `tool.hatch.envs.<name>.python` | `str` | inherits | Python version for this environment |
| `tool.hatch.envs.<name>.dependencies` | `list[str]` | `[]` | Pip-installable dependencies |
| `tool.hatch.envs.<name>.scripts` | `dict[str,str\|list]` | `{}` | Named runnable scripts |
| `tool.hatch.envs.<name>.env-vars` | `dict[str,str]` | `{}` | Environment variables injected at runtime |
| `tool.hatch.build.targets.wheel.packages` | `list[str]` | auto | Source packages to include in the wheel |
| `tool.hatch.build.targets.sdist.include` | `list[str]` | auto | Paths to include in the sdist |
| `tool.hatch.build.targets.sdist.exclude` | `list[str]` | `[]` | Paths to exclude from the sdist |
| `tool.hatch.build.hooks.custom.path` | `str` | — | Path to custom build hook module |
| `tool.hatch.publish.index.repo` | `str` | `"main"` | PyPI repo alias (`main` or `test`) |
| `tool.hatch.metadata.allow-direct-references` | `bool` | `false` | Allow VCS/URL dependencies |

---

## Publish Configuration

```toml
[tool.hatch.publish.index]
repo = "main"
```

Publish to TestPyPI:

```bash
hatch publish -r test
```

!!! warning "Credentials"
    Never commit PyPI tokens or passwords to source control. Use environment variables:
    `HATCH_INDEX_USER` and `HATCH_INDEX_AUTH`.

---

## Integration with `readthedocs`

```yaml
# .readthedocs.yaml
version: 2

build:
  os: ubuntu-24.04
  tools:
    python: "3.13"

mkdocs:
  configuration: mkdocs.yml

python:
  install:
    - requirements: docs/requirements.txt
```

---

## Related

- [Getting Started](getting-started.md) — first steps
- [API Reference](api-reference.md) — programmatic interface
