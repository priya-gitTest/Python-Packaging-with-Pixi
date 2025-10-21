---
title: "Why Python Packages?"
teaching: 15
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- Why must we package our Python code?
- What precisely may be packaged?
- What is the Python Package Index (PyPI), and what purpose does it serve?
- What is a build?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- To understand the benefits of Python packaging.
- To determine whether packaging is suitable for your use case.
- To acquire knowledge of components of Python packaging such as PyPI.
- To become familiar with the build process.

::::::::::::::::::::::::::::::::::::::::::::::::
<img width="983" height="974" alt="image" src="https://github.com/user-attachments/assets/5df6c1a0-bee9-4b38-99e3-725ada1b5d3c" />
 Ref : https://xkcd.com/1987/

 
## Introduction
Software development is a creative pursuit, and it is satisfying to write code that solves interesting problems. However, once our code is ready, how can we share it globally? This course provides instruction in how to distribute Python code using Pixi. You might liken a package to the old-style setup.exe: a standardised method of distributing software.

By packaging code, you address several important challenges, including ensuring reproducibility, achieving cross-platform compatibility, and supporting multiple environments. Distributing code as a package offers many advantages over merely sharing source files, for example via GitHub:

Dependency management: A package can explicitly declare its dependencies. Tools such as pip (or uv) can then automatically install them for the user.

Versioning: You may version your package and distribute multiple versions, thereby supporting backwards compatibility.

Standardisation: Packaging is the established method of distributing code via recognised repositories such as PyPI.

Metadata: Packages include project-specific metadata, which is essential for end users.

## Steps to create a Python Package :
<img width="1298" height="250" alt="image" src="https://github.com/user-attachments/assets/be6f94ec-599b-4a1e-bd5b-63c2dfad720c" />


  ## What may be packaged ?

  Any .py files (modules) or directories with __init__.py (packages) can be packaged..

  ## What is PyPI

  PyPI is the repository where all released Python packages are made available for end users. You may explore it here: [PyPI](https://pypi.org/). 
There is also [TestPyPI](https://test.pypi.org/), a repository which allows us to experiment with distribution tools and procedures without affecting the live PyPI. In this course, we will publish our package to TestPyPI.

  ## What is a Build ?

  A build is the process by which your project’s source code is transformed into a distributable format. These build artefacts can then be installed using tools such as `pip`.
 A build may be created using the command in the terminal : 
 ```bash
python -m build
```
 The successful build process produces files such as a **wheel** (`.whl`) or a **source archive** (`.tar.gz`), which can be installed via `pip` or uploaded to PyPI. It is vital to version your build and supply the requisite metadata.

::::::::::::::::::::::::::::::::::::: keypoints

- The code must be versioned.
- Project dependencies must be managed.
- The project’s metadata must be clearly defined.
- To make Python code installable, reusable and distributable via PyPI or TestPyPI, one must package the code.

::::::::::::::::::::::::::::::::::::::::::::::::
