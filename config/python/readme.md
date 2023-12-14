# Snippets

## `pyproject.toml`

### Package

About classifiers: https://pypi.org/classifiers/

```toml
[build-system]
requires = ["setuptools>=61.0.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "NAME"
description = "DESCRIPTION"
keywords = ["KEYWORDS"]
classifiers = [
    "Development Status :: 5 - Production/Stable",
    "Environment :: Console",
    "Intended Audience :: Science/Research",
    "Operating System :: OS Independent",
    "Programming Language :: Python :: 3",
]
requires-python = ">=3.10"
dynamic = ["version", "readme", "dependencies"]

[tool.setuptools.dynamic]
version = { attr = "mediasub.__version__" }
dependencies = { file = ["requirements.txt"] }
readme = { file = ["README.md"] }

[tool.setuptools]
packages = [""]  # FILL HERE

[tool.setuptools.package-data]
mediasub = ["py.typed"]
```

### bandit

```toml
[tool.bandit]
skips = ["B101"]
```

### black

```toml
[tool.black]
line-length = 120
```

### isort

```toml
[tool.isort]
profile = "black"
combine_as_imports = true
combine_star = true
line_length = 120
```

### pylint

```toml
[tool.pylint]
max-line-length = 120
allow-reexport-from-package = true
ignore-patterns = [".*.pyi"]
jobs = 4
unsafe-load-any-extension = false
disable = [
    "missing-module-docstring",
    "missing-class-docstring",
    "missing-function-docstring",
    "abstract-method",
    # "arguments-differ",
    # "attribute-defined-outside-init",
    # "duplicate-code",
    # "eq-without-hash",
    # "fixme",
    # "global-statement",
    # "implicit-str-concat",
    # "import-error",
    # "import-self",
    # "import-star-module-level",
    # "inconsistent-return-statements",
    # "invalid-str-codec",
]
argument-rgx = "^[a-z_][a-z0-9_]{0,30}$"
attr-rgx = "^[a-z_][a-z0-9_]{0,30}$"
function-rgx = "^[a-z_][a-z0-9_]{0,30}$"
method-rgx = '[a-z_][a-z0-9_]{0,30}$'
variable-rgx = '[a-z_][a-z0-9_]{0,30}$'
ignore-long-lines = '''(?x)(
^\s*(\#\ )?<?https?://\S+>?$|
^\s*(from\s+\S+\s+)?import\s+.+$)'''
indent-string = '    '
dummy-variables-rgx = '^\*{0,2}(_$|unused_|dummy_)'
callbacks = ['cb_', '_cb']
```

### tox

Adapt to your needs!

```toml
[tool.tox]
legacy_tox_ini = """
[tox]
skipsdist = true

[testenv]
deps =
    -r requirements.txt
    -r requirements-dev.txt
commands =
    pytest
    black --check src/
    bandit -r src/ tests/ -c pyproject.toml
    isort ./src/ --check
    pyright src/
"""
```

# Example

`pyproject.toml`

```toml
[tool.bandit]
skips = ["B101"]

[tool.black]
line-length = 120

[tool.isort]
profile = "black"
combine_as_imports = true
combine_star = true
line_length = 120

[tool.pylint]
max-line-length = 120
allow-reexport-from-package = true
ignore-patterns = [".*.pyi"]
jobs = 4
unsafe-load-any-extension = false
disable = [
    "missing-module-docstring",
    "missing-class-docstring",
    "missing-function-docstring",
    "abstract-method",
    # "arguments-differ",
    # "attribute-defined-outside-init",
    # "duplicate-code",
    # "eq-without-hash",
    # "fixme",
    # "global-statement",
    # "implicit-str-concat",
    # "import-error",
    # "import-self",
    # "import-star-module-level",
    # "inconsistent-return-statements",
    # "invalid-str-codec",
]
argument-rgx = "^[a-z_][a-z0-9_]{0,30}$"
attr-rgx = "^[a-z_][a-z0-9_]{0,30}$"
function-rgx = "^[a-z_][a-z0-9_]{0,30}$"
method-rgx = '[a-z_][a-z0-9_]{0,30}$'
variable-rgx = '[a-z_][a-z0-9_]{0,30}$'
ignore-long-lines = '''(?x)(
^\s*(\#\ )?<?https?://\S+>?$|
^\s*(from\s+\S+\s+)?import\s+.+$)'''
indent-string = '    '
dummy-variables-rgx = '^\*{0,2}(_$|unused_|dummy_)'
callbacks = ['cb_', '_cb']

[tool.tox]
legacy_tox_ini = """
[tox]
skipsdist = true

[testenv]
deps =
    -r requirements.txt
    -r requirements-dev.txt
commands =
    pytest
    black --check src/
    bandit -r src/ tests/ -c pyproject.toml
    isort ./src/ --check
    pyright src/
"""
```
