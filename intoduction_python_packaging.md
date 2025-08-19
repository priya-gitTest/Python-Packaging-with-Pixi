---
title: "Why Python Packages?"
teaching: 15
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- Why do you need to package your python code?
- What can you actually package?
- What is Python Package Index (PyPI) and its purpose?
- What is a build?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- benefits of python packaging
- does it fit your use case
- understand some componets of python packaing like PyPi
- understand the build process

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction
We all love to write code, to solve interesting problems. What if we have our code ready and we want to share it across the world. Well there are many ways to do that ofcourse ! By doing this course we will learn to distribute our code via Python Packaging using a tool call Pixi. You can think of the package as setup.exe from yester years.

When we make a package, we solve some key challenges like reproducibility, making it platform independent and also make it multi- environment.
Distributing our code as package is better than sharing the souce code via for instance in a Github repository for many reasons :

- Dependency management : A Package can explicityl declare its deepndencies. Tools like 'pip' or 'uv' can be then used to automatically install them for a user.
- Versioning : You version your package and can make and distribute several versions of your code for backwards compatability.
- Standerdisation : Packaging is an accepted way to distribute the code via repositories like PyPI
- Metadata : A package has project specific metadata which are important for the end users.

  ## What can you package ?

  Any .py files (modules) or directories with __init__.py (packages).

  ## What is PyPI

  PyPi is the repository where all the Python packages which are released are available for end users to use.
  You can visit it here to have a look : https://pypi.org/
  There is also a repository called https://test.pypi.org/, which allows us to try distribution tools and processes without affecting the real PyPi.
  In this course , we will publish our package to TestPyPI.

  ## What is a build ?

  It can be defined as a process of creation of distribution of your project from source code. This distribution can then be installed using tools like 'pip' or 'uv' etc.
  You can create a build for your project using the following command in the terminal : python -m build.

  The end product of a successful build process in a .whl or .tar.gz file. These can then be installed via pip or uploaded to PyPI.
  It is important to version your build and provide necessary metadata.

::::::::::::::::::::::::::::::::::::: keypoints

- TBD

::::::::::::::::::::::::::::::::::::::::::::::::
