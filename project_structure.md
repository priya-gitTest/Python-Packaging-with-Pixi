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
This create a following structure for us. 

<img width="301" height="96" alt="image" src="https://github.com/user-attachments/assets/b07a9498-cd76-470b-80ad-d74a5202c061" />

`pixi.toml` : Lets view and edit the pixi.toml file generated for us.

```toml
[project]
authors = ["Priyanka O"]
name = "greet_me"
version = "0.1.0"
platforms = ["linux-64"]
description = "A simple greeting package."

[dependencies]
python = ">=3.10"

```
 

Lets install the dependencies now, which wiil generate the `pixi.lock` file
```bash
pixi install
```
```output
▪ fetching repodata    [━━━━━━━━━━━━━━━━━━━━] 
▪ solving              [━━━━━━━━━━━━━━━━━━━━]  1/1
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
