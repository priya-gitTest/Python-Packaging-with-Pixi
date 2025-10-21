---
title: "Extra"
teaching: 15
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- How can we use `pixi run start`?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn how to use Pixi to run your project.

::::::::::::::::::::::::::::::::::::::::::::::::
 
## Introduction

After cloning a project, Pixi makes it simple to run predefined tasks. If your `pixi.toml` (or `pyproject.toml`) contains a task named start, you can execute it directly using:

`git clone project.git && cd project`

`pixi run start`

This command will:
- Ensure that the required environment is installed (creating or updating it if necessary).
- Run the start task exactly as defined in your configuration file.

This provides a convenient and reproducible way to launch your project without needing to manually manage dependencies or commands.

::::::::::::::::::::::::::::::::::::: keypoints
- Define tasks such as `start` in your `pixi.toml` or `pyproject.toml`.
- Use `pixi run <task-name>` to execute those tasks.
- `pixi run start` ensures consistency and reproducibility when launching a project.

::::::::::::::::::::::::::::::::::::::::::::::::
