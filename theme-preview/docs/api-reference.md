# API Reference

This page tests **typed Python signatures**, **parameter tables**, and mixed admonition usage typical in API docs.

---

## `hatch.env`

### `Environment`

```python
class Environment:
    """Represents a managed virtual environment."""

    name: str
    python: str
    dependencies: list[str]
    env_vars: dict[str, str]

    def __init__(
        self,
        name: str,
        python: str = "3.12",
        dependencies: list[str] | None = None,
        env_vars: dict[str, str] | None = None,
    ) -> None: ...
```

#### Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `name` | `str` | — | Unique environment name (e.g. `"default"`, `"test"`) |
| `python` | `str` | `"3.12"` | Python version string used to resolve the interpreter |
| `dependencies` | `list[str] \| None` | `None` | PEP 508 dependency specifiers; `None` means empty |
| `env_vars` | `dict[str, str] \| None` | `None` | Key/value pairs injected at runtime |

!!! info "Inheritance"
    When `python` is `None`, the environment inherits the Python version from the `default` environment. If `default` also has no explicit version, the active interpreter at `hatch shell` invocation time is used.

---

### `Environment.create()`

```python
def create(self, *, purge: bool = False) -> None:
    """Create the virtual environment on disk.

    Args:
        purge: If ``True``, delete and recreate the environment
            even when it already exists.

    Raises:
        EnvironmentExistsError: When the environment already exists
            and ``purge`` is ``False``.
        PythonNotFoundError: When the requested Python version
            cannot be located.
    """
```

!!! warning "Idempotency"
    Calling `create()` on an existing environment without `purge=True` raises `EnvironmentExistsError`. Check `environment.exists()` first if you want conditional creation.

---

### `Environment.remove()`

```python
def remove(self) -> None:
    """Remove the virtual environment from disk.

    Raises:
        EnvironmentNotFoundError: If the environment does not exist.
    """
```

---

### `Environment.run()`

```python
def run(
    self,
    args: list[str],
    *,
    cwd: str | os.PathLike | None = None,
    env: dict[str, str] | None = None,
    capture_output: bool = False,
) -> subprocess.CompletedProcess[str]:
    """Execute a command inside the environment.

    Args:
        args: Command and arguments as a list, e.g. ``["pytest", "-v"]``.
        cwd: Working directory for the subprocess. Defaults to the
            current working directory.
        env: Additional environment variables merged with the
            environment's own ``env_vars``. Keys in ``env``
            take precedence.
        capture_output: When ``True``, stdout and stderr are captured
            and returned rather than streamed to the terminal.

    Returns:
        A :class:`subprocess.CompletedProcess` instance.

    Raises:
        EnvironmentNotFoundError: If the environment does not exist.
        subprocess.CalledProcessError: If the command exits with a
            non-zero return code.
    """
```

#### Example

```python
from hatch.env import Environment

env = Environment(name="test", dependencies=["pytest>=8"])
env.create()

result = env.run(["pytest", "tests/", "-q"], capture_output=True)
print(result.stdout)
```

---

## `hatch.version`

### `get_version()`

```python
def get_version(path: str | os.PathLike) -> str:
    """Read the version string from a ``pyproject.toml`` file.

    Args:
        path: Path to the ``pyproject.toml`` file, or a directory
            containing one.

    Returns:
        The version string (e.g. ``"1.2.3"`` or ``"2.0.0b1"``).

    Raises:
        FileNotFoundError: If no ``pyproject.toml`` is found.
        KeyError: If the ``[project]`` table has no ``version`` key and
            version is not listed in ``dynamic``.
    """
```

### `bump_version()`

```python
def bump_version(
    path: str | os.PathLike,
    part: Literal["major", "minor", "patch"],
    *,
    commit: bool = False,
    tag: bool = False,
) -> str:
    """Bump the version component and optionally commit and tag.

    Args:
        path: Path to ``pyproject.toml``.
        part: Which version segment to increment.
        commit: If ``True``, create a git commit with the message
            ``chore: bump version to <new_version>``.
        tag: If ``True`` (and ``commit`` is also ``True``), create an
            annotated git tag ``v<new_version>``.

    Returns:
        The new version string after bumping.
    """
```

!!! danger "Irreversible without VCS"
    `bump_version` modifies `pyproject.toml` in-place. Without version control, the old version cannot be recovered. Always run inside a git repository.

---

## `hatch.build`

### `build()`

```python
def build(
    targets: list[Literal["wheel", "sdist"]] | None = None,
    *,
    clean: bool = False,
    output_dir: str | os.PathLike = "dist",
) -> list[Path]:
    """Build distribution artifacts.

    Args:
        targets: List of build targets. Defaults to ``["wheel", "sdist"]``
            when ``None``.
        clean: Remove existing artifacts in ``output_dir`` before building.
        output_dir: Directory to write built artifacts into.

    Returns:
        List of :class:`pathlib.Path` objects pointing to the built files.
    """
```

#### Example

```python
from hatch.build import build

artifacts = build(targets=["wheel"], clean=True)
for artifact in artifacts:
    print(f"Built: {artifact}")
# Built: dist/my_project-1.2.3-py3-none-any.whl
```

---

## Exceptions

| Exception | Module | Raised when |
|-----------|--------|-------------|
| `EnvironmentExistsError` | `hatch.env` | `create()` called on an existing env without `purge=True` |
| `EnvironmentNotFoundError` | `hatch.env` | `remove()` or `run()` called on a non-existent env |
| `PythonNotFoundError` | `hatch.env` | Requested Python version cannot be located |
| `VersionNotFoundError` | `hatch.version` | `pyproject.toml` has no resolvable version |
| `BuildError` | `hatch.build` | Build process exits with non-zero code |

---

*Back to [Getting Started](getting-started.md) or [Configuration](configuration.md).*
