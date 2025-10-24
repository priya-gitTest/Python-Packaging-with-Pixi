---
title: "Why choose Pixi for Python Packaging ?"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions

- Why use Pixi?
- What are the benefits of Pixi ?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand the advantages offered by Pixi.
-  To learn about `pixi.toml` and `pyproject.toml`
-  To understand the role of `pixi.lock`.
-  To explore the concept of multi-environment support.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Pixi is a fast, modern and reproducible package management tool. It has lots of [features](https://pixi.sh/latest/#what-is-the-difference-with-pixi) which are not all present in a single tool at this point in time. These capabilities make Pixi an attractive choice for managing Python and multi-language projects.

Key features include:

- **Support for both PyPI and Conda packages**: enabling flexibility in sourcing dependencies.
- **Performance**: lightweight and modern, designed for speed.
- **Multi-language dependency management**: e.g. Python with Rust, or Python with C/C++.
- **Integration with `uv`**: leveraging a high-performance package installer.
- **Reproducibility**: guaranteed through the use of `pixi.lock`.
- **Configuration via TOML files**: supports both `pixi.toml` and `pyproject.toml`.
   
## Configuration files (`pixi.toml` and `pyproject.toml`)

`pixi.toml`: The configuration file used by Pixi to define environments, dependencies, and tasks.
`pyproject.toml`: A standard configuration file within the Python ecosystem (PEP 518/621). It is required by build tools such as Poetry, Hatch, Flit, and setuptools. This file specifies project metadata (e.g. name, version, author) as well as dependencies and build settings.

## Multi-environment support

Pixi allows you to define dependencies for specific operating systems (e.g. Windows, macOS, Linux) or for distinct environments such as development, testing, and production. This makes it easier to tailor the project configuration to match the context in which the software is being deployed or developed.

## pyproject.toml
For this demo, we will mainly focus on `pyproject.toml` file.
We make this choice due to following specifications and recomendations : [PEP 621](https://peps.python.org/pep-0621/), [PEP 517](https://peps.python.org/pep-0517/), and [PEP 660](https://peps.python.org/pep-0660/).

You can also read at these links: 

- https://pixi.sh/v0.40.1/reference/pixi_manifest/#pypi-dependencies
- https://pixi.sh/v0.40.1/advanced/pyproject_toml/

::::::::::::::::::::::::::::::::::::: keypoints

- Choose a tool with good support and long term vision.
- Choose a tool suitable for your project.
- Focus on  PEP specifications and recomendations.
  
::::::::::::::::::::::::::::::::::::::::::::::::
