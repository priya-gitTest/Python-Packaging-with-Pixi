---
title: "Metadata for Python packging"
teaching: 5
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- What is `pyproject.toml`?
- 

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand the structure of `pyproject.toml`

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

In the previos lesson, we touched upon `pixi.toml` briefly. In this lesson, we will learn about `pyproject.toml`.
`pyproject.toml` is the most common format for Python projects.
Please not, for a project maintained using pixi, either of the 2 i.e. `pyproject.toml` or `pixi.toml` are fine. You just need to take care of some specific syntaxes.

To add `pyproject.toml` file, we give the following command : 
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
The `[build-system]` table in a pyproject.toml file tells packaging tools like pip what software is needed to build your Python project. It specifies the build backend that will be used to create distributable packages, like wheels (.whl) or source distributions (.sdist).

This section was introduced by PEP 518 and is essential for modern Python packaging.
The `[build-system]` table has two main keys:

1. `requires`: This is a list of strings specifying the packages needed to build your project. These packages will be downloaded and installed into a temporary, isolated environment before the build process begins. You must include the build backend itself here.
2. `build-backend`: This is a string that points to the specific Python object (the "backend") that packaging tools will use to execute the build. It's the entry point for creating your project's packages.
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
  
  `[tool.pixi.pypi-dependencies]` : Thus section is used to delare the depencecis of our project that come from Python Package Index. In short they are libraries necessary for our project and will be installed via pip.

```toml
[project]
name = "greet_me"
requires-python = ">=3.10"

[tool.pixi.workspace]
channels = ["conda-forge"]
platforms = ["linux-64", "win-64"]

[tool.pixi.pypi-dependencies]
requests = ">=2.31.0,<3"
```
You can specify a range or multiple supported Python versions using the syntax below.
```toml
requires-python = ">=3.10, <3.12"
```
If you were using `pixi.toml` file, the equivalent syntax would be 
```toml
[workspace]
name = "greet_me"
channels = ["conda-forge"]
platforms = ["linux-64", "win-64"]

[dependencies]
python = ">=3.10"
```
- Tasks

Here you can specify various steps that you would want to run before making your package. It ususally lets you define and run custom cammands or scripts for your project.
```toml
[tool.pixi.tasks]
# This command will only be defined on Windows
greet  = { cmd = "echo 'Happy Python Packaging!'" }
```
::::::::::::::::::::::::::::::::::::: keypoints
- Need to have a `pyproject.toml` file
- Need to have `[build-system]` section  with `requires` and `build-backend` specfied.
- Need to have `[project]` section with atleast `name` and `version` specified.
- Nice to have `dependencies` specified in `[project]` section.
  
::::::::::::::::::::::::::::::::::::::::::::::::
