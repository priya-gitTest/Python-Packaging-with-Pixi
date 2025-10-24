---
title: Setup
---

<!--FIXME: Setup instructions live in this document. Please specify the tools and
the data sets the Learner needs to have installed.

## Data Sets


FIXME: place any data you want learners to use in `episodes/data` and then use
       a relative link ( [data zip file](data/lesson-data.zip) ) to provide a
       link to it, replacing the example.com link.

Download the [data zip file](https://example.com/FIXME) and unzip it to your Desktop -->

## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Details

For this course, we will use **GitHub Codespaces**, which provides a cloud-based development environment that runs directly in your web browser.

This approach means that no software installation is required on your personal computer, making it much easier to get started.

Your Codespace environment will be **Linux-based**, so we will be using standard Linux commands and tools throughout the lessons.

:::::::::::::::::::::::::::::::::::::::::::::::::::

### Create a repository 

- Log into [GitHub](https://github.com) and create a new repository for this lesson called `greet_me` and add a Licence File when creating the repository. In this case it doesn't matter which licence (this is just a practice repo) - we just need something to initialise the repo, and a licence to satisfy the TestPyPI requirements.

- From the repository page, open the **Code** dropdown menu, select the **Codespaces** tab, and click **Create codespace on main**.

<img width="416" height="353" alt="image" src="https://github.com/user-attachments/assets/15167dca-b8c3-4701-87ac-3d6cb2b1022b" />

If you get an error (e.g. "Oh no, it looks like you are offline!") try a different browser or incognito mode.

 - Once your Codespace has been created, open the terminal inside it and run the following commands.

### Install Pixi

Run the following

```bash
curl -fsSL https://pixi.sh/install.sh | sh
```
```output
This script will automatically download and install Pixi (latest) for you.
Getting it from this url: https://github.com/prefix-dev/pixi/releases/latest/download/pixi-x86_64-unknown-linux-musl.tar.gz
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 23.2M  100 23.2M    0     0  24.0M      0 --:--:-- --:--:-- --:--:-- 66.9M
The 'pixi' binary is installed into '/home/codespace/.pixi/bin'
Updating '/home/codespace/.bashrc'
Please restart or source your shell.
```
If required, restart your shell:
```bash
source ~/.bashrc
```
Verify that Pixi has been installed correctly.
_Please note: the version number displayed may differ from the example below, as newer releases may have been published since this course was written._
```bash
pixi --version
```
```output
pixi 0.57.0
```

