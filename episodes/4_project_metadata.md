---
title: "Metadata for Python packging"
teaching: 5
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- What is `pyproject.toml`?
- What is a lockfile, and why is it necessary? 

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand the structure and purpose of `pyproject.toml`
- To appreciate the role and necessity of a lockfile.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

In the previous lesson, we briefly looked into `pyproject.toml`. In this lesson, we shall focus a bit more in detail on `pyproject.toml`, which is the most widely used configuration format for Python projects.
Please note, for projects managed with Pixi, either `pyproject.toml` or `pixi.toml` may be employed. The primary distinction lies in syntax, so you need only ensure that you follow the appropriate conventions.

## The `[build-system]` table

This section of a `pyproject.toml` file informs packaging tools such as `pip` which software is required to build your project. It specifies the **build backend** responsible for producing distributable packages such as wheels (`.whl`) or source distributions (`.sdist`).

This section was introduced by **[PEP 518](https://peps.python.org/pep-0518/)** and is essential for modern Python packaging.
It has two main keys:

1. `requires`: A list of packages required to build the project. These are downloaded and installed into a temporary, isolated environment prior to the build process. The build backend itself must also be listed here.
2. `build-backend`: A string reference to the Python object (the “backend”) that will be invoked by packaging tools to create the distributable packages.
   
```toml
[build-system]
requires = ["hatchling"] 
build-backend = "hatchling.build"
```
Some other build tools to read are:
 
- [pdm.backend](https://backend.pdm-project.org) e.g. [fastapi](https://github.com/fastapi/fastapi/blob/cd40c5b40ffd8ba0c6a6a6c96bbf34ec1cf9c525/pyproject.toml#L2)
- [mesonpy](https://mesonbuild.com/meson-python/) e.g. [numpy](https://github.com/numpy/numpy/blob/1d053b3482b178ed057474402ae94c80701796e0/pyproject.toml#L2)
- [setuptools.build_meta](https://setuptools.pypa.io/en/latest/build_meta.html) e.g. [parselmouth](https://github.com/prefix-dev/parselmouth/blob/eb3eda68672ba95871719866403318690e1b37be/pyproject.toml#L3)

  Also, refer to the table [here](https://pixi.sh/latest/concepts/conda_pypi/#tool-comparison)

## Editable Installation

Projects may be installed in editable mode, which allows you to make changes to the source code and have them reflected immediately in the environment without reinstallation. For example, the `greet_me` package we are creating is listed as editable by default.
  
```toml
[tool.pixi.pypi-dependencies]
greet_me = { path = ".", editable = true }
```
  
## Dependency Management
  For dependency handling, the pyproject.toml file should include the requires-python field, which specifies the supported Python versions. For example:
```toml
requires-python = ">=3.11, <3.12"
```
Additional sections in `pyproject.toml` may include:

-  `[tool.pixi.workspace]`: Defines project-wide settings, including package sources and target platforms for resolution.  
-  `[tool.pixi.pypi-dependencies]` : Declares the dependencies to be installed from PyPI (or equivalent sources). These are the external libraries required by the project.

You can specify a range or multiple supported Python versions using the syntax below.
```toml
requires-python = ">=3.11, <3.12"
```

## Classifiers
They are standardized metadata tags that describe your Python package for PyPI and help with filtering and discoverability. You can look for the list of acceptable classifiers [here](https://pypi.org/classifiers/).
They are defined under project section.

```toml
[project]
...
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]
...
```

Final `pyproject.toml` should look like this below, for reference.

```toml
[project]
authors = [{name = "Priyanka Demo", email = "demo@users.noreply.github.com"}]
dependencies = []
name = "greet_me"
requires-python = ">= 3.11"
version = "0.1.0"
description = "greet_me Pixi-managed package"
readme = "README.md"

[build-system]
build-backend = "hatchling.build"
requires = ["hatchling"]

[tool.pixi.workspace]
channels = ["conda-forge"]
platforms = ["linux-64"]

[tool.pixi.pypi-dependencies]
requests = ">=2.32.5,<3"
greet_me = { path = ".", editable = true }

[tool.pixi.tasks]
start = "python -c 'from greet_me import happy; print(happy.greet_happy())'"
```

For insipiration, also check [here](https://github.com/prefix-dev/parselmouth/blob/main/pyproject.toml).

You can read more about `pyproject.toml` [here](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/).

## Lockfiles
A **lockfile** contains the complete set of dependencies, including specific versions, required to reproduce the project environment. It is automatically generated based on the dependencies listed in the `.toml` file, ensuring that builds remain consistent and reproducible.

## Readme
Please add and update the README.md file, in case you havent done so. You can easily generate a README text on [readme.so](https://readme.so/) and copy its content to your READMe file.

::::::::::::::::::::::::::::::::::::: keypoints
- Every project must include a `pyproject.toml` file
- The `[build-system]` section is required and must define both `requires` and `build-backend`.
- The `[project]` section must, at minimum, include the project `name` and `version`.
- It is recommended to specify dependencies in the `[project]` section for clarity and reproducibility.
- Use semantic versioning (MAJOR.MINOR.PATCH) for versioning your packages.
  
::::::::::::::::::::::::::::::::::::::::::::::::
