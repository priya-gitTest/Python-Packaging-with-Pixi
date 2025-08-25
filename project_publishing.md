---
title: "How to publish your Python project"
teaching: 10
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions

- What is Twine and why is it needed
- What is build command and what does it do ?
- How to create and upload the Python package ?
- How to test/ use the uploaded Python package?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn the usage for tools like Twine and build
- How to upload the Python Package to repositories like TestPyPi
- How to use the uploaded package.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction
Once we have created our project, defined all the necessary metadata in the toml file, its time to publish our project. Let see the tools and steps we need to acheive this.
We need to install the following tools
  1. `build` : A tool to read the ['pyproject']toml file and build the package files
     ```bash
     pip install build
     
     python -m build
     ```
     This command creates a dist directory containing two files:
      ```output
      ```
      A wheel file (e.g., my_minimal_package-0.0.1-py3-none-any.whl).

      A source archive (e.g., my-minimal-package-0.0.1.tar.gz).

  2. `twine` :  A tool for securely uploading packages to PyPI and TestPyPI.
   ```bash
   pip install build twine

   twine upload --repository testpypi dist/*
   ```
  You'll be prompted to enter your TestPyPI username and password. It's recommended to use an API token instead of      your password. When prompted for your password, paste the token in.
  
  That's it! After the upload is successful, your package will be available on TestPyPI.

::::::::::::::::::::::::::::::::::::: keypoints


::::::::::::::::::::::::::::::::::::::::::::::::
