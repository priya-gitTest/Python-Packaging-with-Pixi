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
     ```
     ```output
     Collecting build
        Downloading build-1.3.0-py3-none-any.whl.metadata (5.6 kB)
      Requirement already satisfied: packaging>=19.1 in /home/codespace/.local/lib/python3.12/site-packages (from build) (25.0)
      Collecting pyproject_hooks (from build)
        Downloading pyproject_hooks-1.2.0-py3-none-any.whl.metadata (1.3 kB)
      Downloading build-1.3.0-py3-none-any.whl (23 kB)
      Downloading pyproject_hooks-1.2.0-py3-none-any.whl (10 kB)
      Installing collected packages: pyproject_hooks, build
      Successfully installed build-1.3.0 pyproject_hooks-1.2.0
     ```
     ```bash
     python -m build
     ```
     ```output
      * Creating isolated environment: venv+pip...
      * Installing packages in isolated environment:
        - hatchling
      * Getting build dependencies for sdist...
      * Building sdist...
      * Building wheel from sdist
      * Creating isolated environment: venv+pip...
      * Installing packages in isolated environment:
        - hatchling
      * Getting build dependencies for wheel...
      * Building wheel...
      Successfully built greet_me-0.1.0.tar.gz and greet_me-0.1.0-py3-none-any.whl
      ```
     This command creates a `dist` directory containing two files:
     - A wheel file (`greet_me-0.1.0-py3-none-any.whl`).
     - A source archive (`greet_me-0.1.0.tar.gz`).
     
     <img width="259" height="398" alt="image" src="https://github.com/user-attachments/assets/302f502b-34ed-470e-a4e0-884b808a6ff0" />


  3. `twine` :  A tool for securely uploading packages to PyPI and TestPyPI.
   ```bash
   pip install build twine

   twine upload --repository testpypi dist/*
   ```
  You'll be prompted to enter your TestPyPI username and password. It's recommended to use an API token instead of      your password. When prompted for your password, paste the token in.
  
  That's it! After the upload is successful, your package will be available on TestPyPI.

::::::::::::::::::::::::::::::::::::: keypoints


::::::::::::::::::::::::::::::::::::::::::::::::
