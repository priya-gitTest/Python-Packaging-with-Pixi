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
::::::::::::::::::::::::::::::::::::: keypoints
- Define tasks such as `start` in your `pixi.toml` or `pyproject.toml`.
- Use `pixi run <task-name>` to execute those tasks.
- `pixi run start` ensures consistency and reproducibility when launching a project.

::::::::::::::::::::::::::::::::::::::::::::::::
