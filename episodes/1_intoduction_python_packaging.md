---
title: "Why Python Packages?"
teaching: 15
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- Why must we package our Python code?
- What precisely may be packaged?
- Why is __init_.py file important?
- What is the Python Package Index (PyPI), and what purpose does it serve?
- What is a build?


::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand the benefits of Python packaging.
- To determine whether packaging is suitable for your use case.
- To understand the importance of __init_.py file.
- To acquire knowledge of components of Python packaging and understand Python Package Index (PyPI).
- To become familiar with the build process.

::::::::::::::::::::::::::::::::::::::::::::::::
<img width="983" height="974" alt="image" src="https://github.com/user-attachments/assets/5df6c1a0-bee9-4b38-99e3-725ada1b5d3c" />
 Ref : https://xkcd.com/1987/

 
## Introduction
Software development is a creative pursuit, and it is satisfying to write code that solves interesting problems. However, once our code is ready, how can we share it globally? This course provides instruction in how to distribute Python code using Pixi. You might liken a package to the old-style setup.exe: a standardised method of distributing software.

By packaging code, you address several important challenges, including ensuring reproducibility, achieving cross-platform compatibility, and supporting multiple environments. Distributing code as a package offers many advantages over merely sharing source files, for example via GitHub:

- Dependency management: A package can explicitly declare its dependencies. Tools such as pip (or uv) can then automatically install them for the user.
- Versioning: You may version your package and distribute multiple versions, thereby supporting backwards compatibility.
- Standardisation: Packaging is the established method of distributing code via recognised repositories such as PyPI and conda forge.
- Metadata: Packages include project-specific metadata, which is essential for end users.

## Python Package Structure Hierarchy

- Function : A block of reusable code that performs a single specific task.
- Module : A single Python file (.py) that groups related classes,  functions and variables.
- Package : A folder/ collection containing multiple modules and an __init__.py file to organize them.
- The __init__.py files are required to make Python treat folders containing the file as packages
- Library : A collection of related packages or modules that provide broad functionality for reuse.
- Library can have Package(s), which can have module(s) which can have function(s). It can also be considered a Project.
- Python package : A Python package is a collection of related code modules (files) bundled with metadata describing how the package should be installed and used [*](https://pydevtools.com/handbook/explanation/what-is-a-python-package/)

<img width="371" height="659" alt="image" src="https://github.com/user-attachments/assets/32c036e1-246a-4f4c-9072-97bfb39376a7" />


[GIT](https://github.com/psf/requests)
[PyPI](https://pypi.org/project/requests/ )

## Steps to create a Python Package :

<img width="1298" height="250" alt="image" src="https://github.com/user-attachments/assets/be6f94ec-599b-4a1e-bd5b-63c2dfad720c" />


## What may be packaged ?

Any .py files (modules) or directories with __init__.py (packages) can be packaged.


## What is __init__.py file in Python?
The __init__.py file (aka dunder init)  is a Python file that is executed when a package is imported.
It serves two main purposes:

- It marks the directory as a Python Package so that the interpreter can find the modules inside it.
- It can contain initialization code for the Package, such as importing submodules, defining variables, or executing other code.

  [source](https://www.geeksforgeeks.org/python/what-is-__init__-py-file-in-python/)

## What is PyPI

[PyPI](https://pypi.org/) is the repository where all released Python packages are made available for end users.
There is also [TestPyPI](https://test.pypi.org/), a repository which allows us to experiment with distribution tools and procedures without affecting the live PyPI. In this course, we will publish our package to TestPyPI.
You can search PyPI for existing packages to use in your project instead of creating a new one. To make your package easily discoverable, it’s important to provide correct metadata and appropriate [classifiers](https://pypi.org/classifiers/).

## What is a Build ?

A build is the process by which your project’s source code is transformed into a distributable format. These build artefacts can then be installed using tools such as `pip`.
 A build may be created using the command in the terminal : 
 ```bash
python -m build
```
 The successful build process produces files such as a **wheel** (`.whl`) or a **source archive** (`.tar.gz`), which can be installed via `pip` or uploaded to PyPI. It is vital to version your build and supply the requisite metadata.

**Please note**: There are several tools and backends available for building Python packages.

::::::::::::::::::::::::::::::::::::: keypoints

- To make Python code installable, reusable and distributable via PyPI or TestPyPI, one must package the code.
- The Package should have modules (.py file(s)) and __init__.py file.
- The code must be versioned.
- Project dependencies must be managed.
- The project’s metadata must be clearly defined.

::::::::::::::::::::::::::::::::::::::::::::::::
