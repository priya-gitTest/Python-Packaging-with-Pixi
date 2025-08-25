---
title: "Why choose Pixi for Python Packaging ?"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions

- Why Pixi ?
- What are the benefits of Pixi ?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand the benefits offered by Pixi
-  What is `pixi.toml` and `pyproject.toml`
-  What is `pixi.lock`
-  What do we mean by multi-environment support
-  


::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Pixi is a fast and reproducible package management tool. It has lots of [features](https://pixi.sh/latest/#what-is-the-difference-with-pixi) which are not all present in a single tool at this point in time. Hence we choose this tool.
It comes with following features : 

- Native supprt for both PyPI packages and conda
- Modern
- Support for multi-language dependency ( E.g. RUST + Python, or Python + C++)
- Uses `uv` under the hood.
- Helps with reproducibility via `pixi.lock`
   
## Configuration files (`pixi.toml` and `pyproject.toml`)

`pixi.toml` is the file used by Pixi for defining the environment , dependencies and tasks.
`pyproject.toml` is the file in Python ecosystem (PEP 518/621) for configuring the build, distribution and configration of python projects. It is required in build tools like Poetry, Hatch, Flit , setuptools. It specifies metadata (name, version, author). you can also specifiy dependencies here.

## Multi-environment support

You can specify the installation of certain tools and packages specific to a particular OS or environmentsl like ( dev, test prod) etc.


