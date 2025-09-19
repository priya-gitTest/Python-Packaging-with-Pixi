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
- Editable project install

This means that the package is installed in editable mode, so you can make changes to the package and see the changes reflected in the environment, without having to re-install the environment. The `greet_me` package itself is added as an editable dependency.
  
```toml
[tool.pixi.pypi-dependencies]
greet_me = { path = ".", editable = true }
```
  
- Dependency handling
  For dependency management, following lines are necessary in your `pyproject.toml` file. `requires_python` tag is used to specify the version of Python.
  
  `[tool.pixi.workspace]`: This section controls where packages come from and what platforms Pixi should resolve for. It is also used to define project-wide settings.
  
  `[tool.pixi.pypi-dependencies]` : This section is used to delare the dependencies of our project that will be installed via Pip or similar tools from Python Package Index. In short they are libraries necessary for our project and will be installed via pip.

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

Here you can specify various steps that you would want to run before making your package. It ususally lets you define and run custom commands or scripts for your project. You can specify `inputs`, `outputs` or `depends-on` tasks.

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
A lockfile contains everything needed to reproduce the project environment. It is generated from the dependencies specified in the `.toml` file.

::::::::::::::::::::::::::::::::::::: keypoints
- Need to have a `pyproject.toml` file
- Need to have `[build-system]` section  with `requires` and `build-backend` specfied.
- Need to have `[project]` section with atleast `name` and `version` specified.
- Nice to have `dependencies` specified in `[project]` section.
  
::::::::::::::::::::::::::::::::::::::::::::::::
