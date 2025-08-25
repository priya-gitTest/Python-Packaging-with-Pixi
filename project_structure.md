---
title: "Set up a project directory"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions

- How should we  structure our project ?
- What is __init__.py ?
- How should be name our packages ?
  

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand how to structure your project to be able to package it well.
- Understand the importance of  __init__.py and where to place it.
- Giving unique but understandable names to our packages.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

It is important to structure your project properly and include the necessary files, while giving unique yet understandable package names.

Packages are a way to organize modules in a Python project. A project can contain several modules, and grouping them into packages helps keep the code organized and maintainable.

Every package should have a special file called __init__.py in its folder. The presence of this file signals to Python that the folder is a package, allowing it to be imported later in your code.

## Project Structure
A typical project would look like :
```greet_me/
└── my_package/
    ├── __init__.py
    ├── happy.py
    └── sad.py
```
Lets create the same structure for our project in the codespace.
```bash
pixi init greet_me
```
```output
✔ Created ...greet_me/pixi.toml
```

This create a following structure for us. 

<img width="301" height="96" alt="image" src="https://github.com/user-attachments/assets/b07a9498-cd76-470b-80ad-d74a5202c061" />

`pixi.toml` : Lets view and edit the pixi.toml file generated for us.

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
Lets go inside the project directory:
```bash
cd greet_me
```

To add libraries via pixi command use this syntax : 
```bash
pixi add requests
```
```output
✔ Added requests >=2.32.5,<3
```
Let us see that gets added to the pixi.toml

```toml
[dependencies]
requests = ">=2.32.5,<3"
```
You can also generate/ update `pixi.lock` file via this command : 
```bash
pixi lock
```
```output
✔ Lock-file was already up-to-date
```
Alternatively, Lets install the dependencies now, which wiil generate the `pixi.lock` file. This is also useful when you clone someone else repo, the dependencies are installed via the `pixi.lock` file
```bash
pixi install
```
```output
✔ The default environment has been installed.
```
There is also a command to update your dependencies to newer versions where possible with latest compatible versions. 
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
Ultimately, our project structure should look like this : 
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
Add the following task to the pixi.toml file and then run via pixi

```toml

[tasks]
start = "python -c 'from my_package  import happy; print(happy.greet_happy())'"
```

```bash
pixi run start
```
```output
Yay! happy day! 😀
```
::::::::::::::::::::::::::::::::::::: keypoints
- Follow the folder structure
- dont forget to add the __init__.py file.
- Sequence of pixi commands : init -> add -> run -> lock ->install -> update
  
::::::::::::::::::::::::::::::::::::::::::::::::
