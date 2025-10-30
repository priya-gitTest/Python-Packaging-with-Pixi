---
title: "Extra"
teaching: 1
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- How can we use `pixi run start`?
- How to yank or un-yank a release?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn how to use Pixi to run your project.
- Learn how to make a release unavialable or undo that.

::::::::::::::::::::::::::::::::::::::::::::::::
 
## Introduction

After cloning a project, Install Pixi and Pixi makes it simple to run predefined tasks. If your `pixi.toml` (or `pyproject.toml`) contains a task named start, you can execute it directly using:

```bash
gh repo clone priya-gitTest/greet_me && cd greet_me
curl -fsSL https://pixi.sh/install.sh | sh
```
If required, restart your shell:
```bash
source ~/.bashrc
```
Verify that Pixi has been installed correctly.
```bash
pixi --version
```
Now run
```bash
pixi run start
```
```output
✨ Pixi task (start): python -c 'from greet_me1 import happy; print(happy.greet_happy())'                             
Yay! happy day! 😀
```

This command will:

- Ensure that the required environment is installed (creating or updating it if necessary).
- Run the start task exactly as defined in your configuration file.

This provides a convenient and reproducible way to launch your project without needing to manually manage dependencies or commands.
You can check the example project [here](https://github.com/priya-gitTest/greet_me)

## Yank and Un-yank
Occasionally, a release may contain an error or be uploaded by mistake. While PyPI and TestPyPI don’t allow deleting releases for security and reproducibility reasons, you can mark a specific version as yanked.
Yanked releases remain accessible for reproducibility but are ignored by default when users install packages with `pip install <package-name>`.

Steps to Yank a version of your Python Package:

- Log into your PyPI or TestPyPI account
- Click on the your Projects from the top right location under your user-name.
  <img width="708" height="439" alt="image" src="https://github.com/user-attachments/assets/25d8773a-1912-407c-8338-8e3d10150328" />

- Select the right project /package from the options shown and click on the **Manage** button.
  <img width="1295" height="633" alt="image" src="https://github.com/user-attachments/assets/1aa1cffa-9961-4f2b-aae3-c6b18c90f331" />

- Select the version you wish to yank and choose that option by clicking on the **Options** button and select **Yank**. 
  <img width="1298" height="644" alt="image" src="https://github.com/user-attachments/assets/554d4387-18ff-4e34-829f-759a9671bbcc" />

- You will be shown a pop-up. Fill the version nos and your releace will not be yanked.
  <img width="602" height="795" alt="image" src="https://github.com/user-attachments/assets/eca2232d-0fb9-42e7-b080-afb4f3da9f23" />


- Once your release is yanked, it be be shown like below.
  <img width="1279" height="297" alt="image" src="https://github.com/user-attachments/assets/740f84ed-e586-487c-8498-90d0378c066d" />


- You can also un-yank it, by clicking on the **Options** and clicking on **Un-yank**.
  <img width="627" height="544" alt="image" src="https://github.com/user-attachments/assets/5a53e6b9-6305-4683-a7af-9b64c2cf9436" />
  
- When you do a `pip install` without stating an explicit verion and no un-yanked versions are available. You may get an error as shown below :
 <img width="1215" height="128" alt="image" src="https://github.com/user-attachments/assets/a70a221f-a1e2-49d8-bf43-5664acc4067d" />


You can read more about Yanking [here](https://docs.pypi.org/project-management/yanking/) and related PEP 592 specification [here](https://peps.python.org/pep-0592/).

## Further Reading

1. [Reproducible Machine Learning Workflows for Scientists with Pixi](https://proceedings.scipy.org/articles/nwuf8465)
   
::::::::::::::::::::::::::::::::::::: keypoints
- Define tasks such as `start` in your `pixi.toml` or `pyproject.toml`.
- Use `pixi run <task-name>` to execute those tasks.
- `pixi run start` ensures consistency and reproducibility when launching a project.
- Yank a faulty release and provide useful comments for why you yanked it.

::::::::::::::::::::::::::::::::::::::::::::::::
