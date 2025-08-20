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

It is important to structure your project and add necessary files and give unique but understanable package names. Packages are a way of structuring modules in a Python Project.
You can have several modules in a project.
Also, every package must have a special file __init__.py in its folder.
The presence of this file, allows the package to be imported later on.

## Project Structure
A typical Project would look like :
```greet_me/
└── my_package/
    ├── __init__.py
    ├── happy.py
    └── sad.py
```
Lets create the same structure for our Project in the codespace.
 
```python
# happy.py
def greet_happy():
    return "Yay! I’m so happy to see you! 😀"
```
```python
# sad.py
def greet_sad():
    return "Oh no… I’m feeling a bit down today. 😢"
```
Ultimately, Our project structure should look like this : 
```greet_me/
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

