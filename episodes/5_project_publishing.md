---
title: "How to publish your Python project"
teaching: 5
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions

- What is Twine and why is it needed
- What is `build` command and what does it do ?
- How can we create and upload a Python package?
- How can we test and use the uploaded Python package?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn how to use tools such as `build` and `twine`.
- Understand how to upload a Python package to repositories such as **TestPyPI**.
- Learn how to install and test an uploaded package.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction
Once a project has been created and all the necessary metadata has been defined in the TOML file, the next step is to **publish** it. This lesson introduces the tools and steps required to achieve this.

The two key tools we need are:

**Build** – for generating distribution files from your project.

**Twine** – for securely uploading those distributions to **PyPI** or **TestPyPI**.

##  Step 1: Create your build

The `build` tool reads your `pyproject.toml` file and generates the package distribution files.

```bash
pixi add --pypi build
```
     
```output
✔ Added build >=1.3.0, <2
Added these as pypi-dependencies.
```
Empty the depenencies under `[project]` and move/edit them to `[tool.pixi.pypi-dependencies]` section, like shown below:

```toml
[project]
dependencies = []

[tool.pixi.pypi-dependencies]
requests = ">=2.32.5,<3"
build = ">=1.3.0,<2"
```
Then run the `build` command:

```bash
pixi run python -m build
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
     
<img width="306" height="533" alt="image" src="https://github.com/user-attachments/assets/503697e4-b93b-45e9-9904-229bd892b47a" />


 ## Step 2 : Create an account on TestPyPI
     
- Visit [TestPyPI](https://test.pypi.org/account/register/) and create an account.
- Generate an **API token** from your account settings.
- Save the token securely, as you will use it during the upload process.
     
<img width="1726" height="625" alt="image" src="https://github.com/user-attachments/assets/0c27a806-8fa2-469a-8b5c-fbf73c47e5e6" />
     

## Step 3: Upload your build
The **Twine** tool is used to securely upload your package distributions.
Install `twine` and modify the `pyroject.toml` file simmilar to what you did for `build` tool above.
 
```bash
pixi add --pypi twine
```

```toml
     [project]
     dependencies = []
     
     [tool.pixi.pypi-dependencies]
     requests = ">=2.32.5,<3"
     build = ">=1.3.0,<2"
```
Now upload the package to TestPyI
```bash
   pixi run twine upload --repository testpypi dist/*
```
  You will be prompted for your TestPyPI API Token, so keep it handy and paste it, when prompted. Use the API token instead of your password by entering `__token__` as the username and pasting the token when prompted for a password.

  ```output
Uploading distributions to https://test.pypi.org/legacy/
WARNING  This environment is not supported for trusted publishing                                                     
Enter your API token: 
Uploading greet_me1-0.1.7-py3-none-any.whl
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.3/4.3 kB • 00:00 • ?
Uploading greet_me1-0.1.7.tar.gz
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.2/12.2 kB • 00:00 • ?

View at:
https://test.pypi.org/project/greet-me1/0.1.7/
  ```

After a successful upload, your package will be available at a URL such as: E.g. : 
`[https://test.pypi.org/project/po-greet-me/0.1.1/](https://test.pypi.org/project/greet-me1/0.1.7/)`

<img width="1743" height="973" alt="image" src="https://github.com/user-attachments/assets/d41cc3d8-1d9a-4a4e-bdaa-a600fe9d2b1a" />


## Handling Errors
If the package name is too similar to an existing project, TestPyPI may return a 403 Forbidden or 400 Bad Request error.
In that case you may end up in an error like this : 

```output
twine upload --repository testpypi dist/*
Uploading distributions to https://test.pypi.org/legacy/
Enter your API token: 
Uploading greet_me-0.1.1-py3-none-any.whl
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.6/2.6 kB • 00:00 • ?
WARNING  Error during upload. Retry with the --verbose option for more details.                                                                                                                                            
ERROR    HTTPError: 403 Forbidden from https://test.pypi.org/legacy/                                                                                                                                                       
    Forbidden
```

This isnt always helpful and you should try this command as tipped in the error message above to know more.

```bash
pixi run twine upload --repository testpypi dist/* --verbose
```

```output
Uploading distributions to https://test.pypi.org/legacy/
INFO     dist/greet_me-0.1.7-py3-none-any.whl (2.3 KB)                                                                
INFO     dist/greet_me-0.1.7.tar.gz (10.7 KB)                                                                         
INFO     username set by command options                                                                              
INFO     Querying keyring for password                                                                                
INFO     No keyring backend found                                                                                     
INFO     Trying to use trusted publishing (no token was explicitly provided)                                          
WARNING  This environment is not supported for trusted publishing                                                     
Enter your API token: 
INFO     username: __token__                                                                                          
INFO     password: <hidden>                                                                                           
Uploading greet_me-0.1.7-py3-none-any.whl
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.2/4.2 kB • 00:00 • ?
INFO     Response from https://test.pypi.org/legacy/:                                                                 
         400 Bad Request                                                                                              
INFO     <html>                                                                                                       
          <head>                                                                                                      
           <title>400 The name 'greet-me' is too similar to an existing project. See                                  
         https://test.pypi.org/help/#project-name for more information.</title>                                       
          </head>                                                                                                     
          <body>                                                                                                      
           <h1>400 The name 'greet-me' is too similar to an existing project. See                                     
         https://test.pypi.org/help/#project-name for more information.</h1>                                          
           The server could not comply with the request since it is either malformed or otherwise incorrect.<br/><br/>
         The name &#x27;greet-me&#x27; is too similar to an existing project. See                                     
         https://test.pypi.org/help/#project-name for more information.                                               
                                                                                                                      
                                                                                                                      
          </body>                                                                                                     
         </html>                                                                                                      
ERROR    HTTPError: 400 Bad Request from https://test.pypi.org/legacy/                                                
         Bad Request                    
```

To fix this, 
- Rename your  Package Folder, [project].name (e.g. from `greet_me` to `greet_me1`) and also change this section, `[tool.pixi.pypi-dependencies]`
  
```toml
[project]
name = "greet-me1" # Changed

[tool.pixi.pypi-dependencies]
requests = ">=2.32.5,<3"
build = ">=1.3.0,<2"
twine = ">=6.2.0,<7"
greet_me1 = { path = ".", editable = true } # Changed

[tool.pixi.tasks]
start = "python -c 'from greet_me1 import happy; print(happy.greet_happy())'" # Changed
```
- Rebuild and upload the package.

```bash
# 1. (Recommended) Remove the old build directory
rm -rf dist

# 2. Re-build your package with the new name
pixi run python -m build

# 3. Upload the new version to TestPyPI
pixi run twine upload --repository testpypi dist/* 
```

## Step 4: Test your package

Create a new Repository with a readme file and install your package from TestPyPI via this command : 

```bash
pip install -i https://test.pypi.org/simple/ greet-me1==0.1.7
```

```output
Looking in indexes: https://test.pypi.org/simple/
Collecting greet-me1==0.1.7
  Downloading https://test-files.pythonhosted.org/packages/92/84/76afd107870f18a144fe5df0cc9fd0d7698c69e82e4c085f2ba339f99218/greet_me1-0.1.7-py3-none-any.whl.metadata (304 bytes)
Downloading https://test-files.pythonhosted.org/packages/92/84/76afd107870f18a144fe5df0cc9fd0d7698c69e82e4c085f2ba339f99218/greet_me1-0.1.7-py3-none-any.whl (2.4 kB)
Installing collected packages: greet-me1
Successfully installed greet-me1-0.1.7
```

Then create a test script : `test_package.py`:

```python
from greet_me1 import happy, sad

print(happy.greet_happy())
```
Run it:
```bash
python test_package.py 
```

```output
Yay! happy day! 😀
```

::::::::::::::::::::::::::::::::::::: keypoints
- Ensure all metadata is filled in and choose a **unique project name**.
- Use `build` to generate distribution files
- Create a TestPyPI account and generate an  **API token**
- Use `twine upload` to securely publish your package.
- Test your package by installing it from TestPyPI via `pip install`.
::::::::::::::::::::::::::::::::::::::::::::::::
