---
title: "Set up a project directory"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions

- How should we  structure our project ?
- What is `__init__.py` ?
- How should be name our packages ?
  

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand how to structure a project effectively in order to package it successfully.
- To recognise the importance of the `__init__.py` file and know where to place it.
- To assign unique yet meaningful names to packages.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

It is essential to structure your project correctly, include the necessary files, and provide packages with names that are both unique and understandable.

Packages are used to organise modules within a Python project. As projects often consist of several modules, grouping them into packages helps to keep the codebase structured, maintainable, and easy to navigate.

Each package must contain a special file named `__init__.py`. The presence of this file indicates to Python that the folder is a package, thereby allowing it to be imported into your code.

## Project Structure
A typical project would look like :
```greet_me/
└── src/my_package/
    ├── __init__.py
    ├── happy.py
    └── sad.py
```
Let us create a similar structure within our codespace.
```bash
pixi init greet_me
```
```output
✔ Created ...greet_me/pixi.toml
```

This generates the following structure:

<img width="301" height="96" alt="image" src="https://github.com/user-attachments/assets/b07a9498-cd76-470b-80ad-d74a5202c061" />

If you prefer to use a `pyproject.toml` file, the following syntax is required (our preferred approach, which will be demonstrated in the next lesson):

```bash
pixi init --format pyproject
```

`pixi.toml` : The initial `pixi.toml` file generated may look like this:

```toml
[workspace]
authors = ["Priyanka O"]
channels = ["conda-forge"]
name = "greet_me"
version = "0.1.0"
platforms = ["linux-64"]
description = "A simple greeting package."

[dependencies]
python = ">=3.10"

[tasks]
```
Change into the project directory:
```bash
cd greet_me
```

To add libraries via Pixi:
```bash
pixi add requests
```
```output
✔ Added requests >=2.32.5,<3
```
This will update the `[dependencies]` section in `pixi.toml`:

```toml
[dependencies]
requests = ">=2.32.5,<3"
```
To generate or update the `pixi.lock` file:
```bash
pixi lock
```
```output
✔ Lock-file was already up-to-date
```
Alternatively, when cloning a repository, you can install dependencies from the `pixi.lock` file:
```bash
pixi install
```
```output
✔ The default environment has been installed.
```
To upgrade dependencies to the latest compatible versions: 
```bash
pixi update
```
```output
▪ solving              [━━━━━━━━━━━━━━━━━━━━]  0/1
▪ updating lock-files    [━━━━━━━━━━━━━━━━━━━━] 0/2
```
```output
✔ Lock-file was already up-to-date
```
## Adding Modules
Create a folder named `my_package` and add three files: `happy.py`, `sad.py`, and `__init__.py`.

```python
# happy.py <- A module
def greet_happy():
    return "Yay! happy day! 😀"
```
```python
# sad.py <- A module
def greet_sad():
    return "Oh no… I’m feeling a bit down today. 😢"
```
The overall project structure should then resemble:
```
greet_me/
├── LICENSE
├── pyproject.toml
├── README.md
├── pixi.toml
├── pixi.lock         # auto-generated, do not edit
├── tests/
│   └── test_greetings.py
└── my_package/
    ├── __init__.py
    ├── happy.py
    └── sad.py
```
## Running a Task
Add the following task to your `pixi.toml` file:

```toml

[tasks]
start = "python -c 'from my_package  import happy; print(happy.greet_happy())'"
```
Then execute:
```bash
pixi run start
```
```output
Yay! happy day! 😀
```
::::::::::::::::::::::::::::::::::::: keypoints
- Follow the appropriate folder structure.
- Always include the `__init__.py` file in packages.
- Sequence of Pixi commands: **init** → **add** → **run** → **lock** → **install** → **update**.
- Define `[project]`, `[tasks]`, and `[dependencies]` in your `pixi.toml` file (or the equivalent in `pyproject.toml`).
  
::::::::::::::::::::::::::::::::::::::::::::::::
