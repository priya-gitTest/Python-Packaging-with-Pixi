---
title: "Metadata for Python packging"
teaching: 5
exercises: 10
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

In the previous lesson, we briefly introduced `pixi.toml`. In this lesson, we shall focus on `pyproject.toml`, which is the most widely used configuration format for Python projects.
Please note, for projects managed with Pixi, either `pyproject.toml` or `pixi.toml` may be employed. The primary distinction lies in syntax, so you need only ensure that you follow the appropriate conventions.

To initialise a project using `pyproject.toml`, run the following command:
```bash
pixi init --format pyproject
```
```output
✔ Created .../greet_me/pyproject.toml
```
## Whats inside `pyproject.toml`

- Manifest metadata
```toml
[project]
name = "greet_me"
version = "0.1.0"
description = "greet_me Pixi-managed package"
authors = [{ name = "Priyanka", email = "" }]
readme = "README.md"
license = { text = "MIT" }
requires-python = ">=3.11"
dependencies = []
```
## The `[build-system]` table

This section of a `pyproject.toml` file informs packaging tools such as `pip` which software is required to build your project. It specifies the **build backend** responsible for producing distributable packages such as wheels (`.whl`) or source distributions (`.sdist`).

This section was introduced by **PEP 518** and is essential for modern Python packaging.
It has two main keys:

1. `requires`: A list of packages required to build the project. These are downloaded and installed into a temporary, isolated environment prior to the build process. The build backend itself must also be listed here.
2. `build-backend`: A string reference to the Python object (the “backend”) that will be invoked by packaging tools to create the distributable packages.
   
```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```
- Editable Installation

Projects may be installed in editable mode, which allows you to make changes to the source code and have them reflected immediately in the environment without reinstallation. For example, the `greet_me` package can be added as an editable dependency.
  
```toml
[tool.pixi.pypi-dependencies]
greet_me = { path = ".", editable = true }
```
  
- Dependency Management
  For dependency handling, the pyproject.toml file should include the requires-python field, which specifies the supported Python versions. For example:
```toml
requires-python = ">=3.11, <3.12"
```
 In a `pixi.toml` file, the syntax would differ slightly, but the purpose remains the same.
 
 Additional sections in `pyproject.toml` may include:
  `[tool.pixi.workspace]`: Defines project-wide settings, including package sources and target platforms for resolution.  
  `[tool.pixi.pypi-dependencies]` : Declares the dependencies to be installed from PyPI (or equivalent sources). These are the external libraries required by the project.

```toml
[project]
name = "greet_me"
requires-python = ">=3.11"

[tool.pixi.workspace]
channels = ["conda-forge"]
platforms = ["linux-64", "win-64"]

[tool.pixi.pypi-dependencies]
requests = ">=2.31.0,<3"
```
You can specify a range or multiple supported Python versions using the syntax below.
```toml
requires-python = ">=3.11, <3.12"
```
If you were using `pixi.toml` file, the equivalent syntax would be 
```toml
[tool.pixi.workspace]
name = "greet_me"
channels = ["conda-forge"]
platforms = ["linux-64", "win-64"]

[tool.pixi.pypi-dependencies]
python = ">=3.11"

[tool.pixi.tasks]
```
- Tasks

The `tasks` section allows you to define custom commands or scripts that should be executed before packaging. These tasks may specify inputs, outputs, or dependencies, enabling you to automate steps in your workflow. You can specify `inputs`, `outputs` or `depends-on` tasks.

```toml
[tool.pixi.tasks]
# This command will only be defined on Windows
greet  = { cmd = "echo 'Happy Python Packaging!'" }
```
Final `pyproject.toml` should look like this below, for reference.

```toml
[project]
authors = [{name = "Priyanka O"}]
dependencies = []
name = "po_greet_me"
requires-python = ">= 3.11"
version = "0.1.2"
description = "greet_me Pixi-managed package"

[build-system]
build-backend = "hatchling.build"
requires = ["hatchling"]

[tool.hatch.build.targets.wheel]
packages = ["my_package"]

[tool.pixi.workspace]
channels = ["conda-forge"]
platforms = ["linux-64"]

[tool.pixi.pypi-dependencies]
greet_me = { path = ".", editable = true }
requests = ">=2.32.5,<3"

[tool.pixi.tasks]
greet  = { cmd = "echo 'Happy Python Packaging!'" }
```
## Lockfiles
A **lockfile** contains the complete set of dependencies, including specific versions, required to reproduce the project environment. It is automatically generated based on the dependencies listed in the `.toml` file, ensuring that builds remain consistent and reproducible.

::::::::::::::::::::::::::::::::::::: keypoints
- Every project must include a `pyproject.toml` file
- The `[build-system]` section is required and must define both `requires` and `build-backend`.
- The `[project]` section must, at minimum, include the project `name` and `version`.
- It is recommended to specify dependencies in the `[project]` section for clarity and reproducibility.
  
::::::::::::::::::::::::::::::::::::::::::::::::
