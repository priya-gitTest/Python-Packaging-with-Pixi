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

::::::::::::::::::::::::::::::::::::: keypoints

- TBD

::::::::::::::::::::::::::::::::::::::::::::::::
