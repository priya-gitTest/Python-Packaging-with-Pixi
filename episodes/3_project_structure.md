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
```
greet_me/
└── src/my_package/
    ├── __init__.py
    ├── happy.py
    └── sad.py
```
Let us create a similar structure within our codespace.
```bash
pixi init --format pyproject
```
```output
✔ Created /workspaces/pixi_demo/pyproject.toml
```

This generates the following structure:

<img width="194" height="213" alt="image" src="https://github.com/user-attachments/assets/cf77b5b3-2b66-413e-9d80-f67ecebc45fa" />


`pyproject.toml` : The initial `pyproject.toml` file generated may look like this:

```toml
[project]
authors = [{name = "Priyanka Demo", email = "demo@users.noreply.github.com"}]
dependencies = []
name = "greet_me"
requires-python = ">= 3.11"
version = "0.1.0"

[build-system]
build-backend = "hatchling.build"
requires = ["hatchling"]

[tool.pixi.workspace]
channels = ["conda-forge"] #Download and install Conda packages from the conda-forge channel
platforms = ["linux-64"]

[tool.pixi.pypi-dependencies] #Add dependencies here which needs to be installed from PyPI
greet_me = { path = ".", editable = true }

[tool.pixi.tasks]
```

To add libraries via Pixi:
```bash
pixi add requests
```
```output
✔ Added requests >=2.32.5,<3
```
This will create/update the `[tool.pixi.dependencies]` section in `pyproject.toml`.

```toml
[tool.pixi.dependencies]
requests = ">=2.32.5,<3"
```
It also generates a `pixi.lock` file which may look somewhat like the image below.

<img width="590" height="262" alt="image" src="https://github.com/user-attachments/assets/3955c422-99ab-4690-a54f-b0c66decfa61" />


To remove a package, use this command and check that `pyproject.toml` is corrected and the package is removed from there.
```bash
pixi remove requests
```
```output
✔ Removed requests
```
To add libraries from PyPI via Pixi:
```bash
pixi add --pypi requests
```
```output
✔ Added requests >=2.32.5, <3
Added these as pypi-dependencies.
```
Check the `pyproject.toml` file. These get added under the `[project]` section 
```toml
[project]
dependencies = ["requests>=2.32.5,<3"]
name = "greet_me"
```
Please note : this wont create a problem when uploading the build but can create problems, when installing the builds.
So best to keep it empty for now and move this to `[tool.pixi.pypi-dependencies]` section , for all projects which need to come from via PyPI namely **build** and **twine** which are used to create and upload build respectively.
```toml
[project]
dependencies = []
name = "greet_me"
...
[tool.pixi.pypi-dependencies]
requests = ">=2.32.5,<3"
greet_me = { path = ".", editable = true }
```

Other commands, that can be later explored : 

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
Lets create these 2 files: `happy.py`, `sad.py` in the folder src/greet_me.

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
├── pixi.lock         # auto-generated, do not edit
└── src/greet_me/
    ├── __init__.py
    ├── happy.py
    └── sad.py
```
<img width="203" height="393" alt="image" src="https://github.com/user-attachments/assets/6acc1213-b9f6-48f9-b385-a3c10268ccd9" />


## Running a Task
Add the following task to your `pyproject.toml` file:

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
- Define / check `[project]`, `[dependencies]` and `[tasks]` in your `pyproject.toml` file .
  
::::::::::::::::::::::::::::::::::::::::::::::::
