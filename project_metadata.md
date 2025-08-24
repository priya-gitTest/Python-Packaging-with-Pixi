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
requires-python = ">=3.10"
dependencies = []
```
```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```
- Editable project install
- Dependency handling
- Tasks
