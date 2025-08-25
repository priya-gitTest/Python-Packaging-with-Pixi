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

For this course, we will use GitHub Codespaces, providing a cloud-based development environment that runs directly in your web browser.
This setup means no local software installation is required on your personal computer, simplifying our getting-started process.
Your Codespace environment is Linux-based, so we will be using standard Linux commands and tools throughout 

:::::::::::::::::::::::::::::::::::::::::::::::::::

## 1. Create a repository 

- Log into [GitHub](https://github.com) and create a new repository for this lesson called `greet_me`.

- From the top right, under the Code drop down, choose the Codepaces tab and click on the button : Create codespace on main.

<img width="416" height="353" alt="image" src="https://github.com/user-attachments/assets/15167dca-b8c3-4701-87ac-3d6cb2b1022b" />

 - Open the terminal inside the codepaces created for you and try the command below.
   
:::::::::::::::: spoiler

### Linux

To install pixi, run:
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
To restart the shell, use this command, if needed.
```bash
source ~/.bashrc
```
Check if pixi is installed correctly
```bash
pixi --version
```
```output
pixi 0.53.0
```
::::::::::::::::::::::::

