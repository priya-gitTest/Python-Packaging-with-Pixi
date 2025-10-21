---
title: "How to publish your Python project"
teaching: 10
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

**Note**: Before proceeding, rename or remove the `pixi.tom`l file, as we will focus on `pyproject.toml`. You may experiment with `pixi.toml` later by removing or renaming `pyproject.toml`.

##  Step 1: Create your build

The `build` tool reads your `pyproject.toml` file and generates the package distribution files.

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


 ## Step 2 : Create an account on TestPyPI
     
- Visit [TestPyPI](https://test.pypi.org/account/register/) and create an account.
- Generate an **API token** from your account settings.
- Save the token securely, as you will use it during the upload process.
     
<img width="1726" height="625" alt="image" src="https://github.com/user-attachments/assets/0c27a806-8fa2-469a-8b5c-fbf73c47e5e6" />
     

## Step 3: Upload your build
The **Twine** tool is used to securely upload your package distributions.
   ```bash
   pip install build twine

   twine upload --repository testpypi dist/*
   ```
  You will be prompted for your TestPyPI username and password. Use the API token instead of your password by entering `__token__` as the username and pasting the token when prompted for a password.

  ```output
Uploading distributions to https://test.pypi.org/legacy/
INFO     dist/po_greet_me-0.1.1-py3-none-any.whl (0.8 KB)                                                                                                                                                                  
INFO     dist/po_greet_me-0.1.1.tar.gz (5.0 KB)                                                                                                                                                                            
INFO     username set by command options                                                                                                                                                                                   
INFO     Querying keyring for password                                                                                                                                                                                     
INFO     No keyring backend found                                                                                                                                                                                          
Enter your API token: 
INFO     username: __token__                                                                                                                                                                                               
INFO     password: <hidden>                                                                                                                                                                                                
Uploading po_greet_me-0.1.1-py3-none-any.whl
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.5/2.5 kB • 00:00 • ?
INFO     Response from https://test.pypi.org/legacy/:                                                                                                                                                                      
         200 OK                                                                                                                                                                                                            
INFO     <html>                                                                                                                                                                                                            
          <head>                                                                                                                                                                                                           
           <title>200 OK</title>                                                                                                                                                                                           
          </head>                                                                                                                                                                                                          
          <body>                                                                                                                                                                                                           
           <h1>200 OK</h1>                                                                                                                                                                                                 
           <br/><br/>                                                                                                                                                                                                      
                                                                                                                                                                                                                           
                                                                                                                                                                                                                           
                                                                                                                                                                                                                           
          </body>                                                                                                                                                                                                          
         </html>                                                                                                                                                                                                           
Uploading po_greet_me-0.1.1.tar.gz
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.7/6.7 kB • 00:00 • ?
INFO     Response from https://test.pypi.org/legacy/:                                                                                                                                                                      
         200 OK                                                                                                                                                                                                            
INFO     <html>                                                                                                                                                                                                            
          <head>                                                                                                                                                                                                           
           <title>200 OK</title>                                                                                                                                                                                           
          </head>                                                                                                                                                                                                          
          <body>                                                                                                                                                                                                           
           <h1>200 OK</h1>                                                                                                                                                                                                 
           <br/><br/>                                                                                                                                                                                                      
                                                                                                                                                                                                                           
                                                                                                                                                                                                                           
                                                                                                                                                                                                                           
          </body>                                                                                                                                                                                                          
         </html>                                                                                                                                                                                                           

View at:
https://test.pypi.org/project/po-greet-me/0.1.1/
  ```

After a successful upload, your package will be available at a URL such as: E.g. : 
`https://test.pypi.org/project/po-greet-me/0.1.1/`

<img width="1619" height="854" alt="image" src="https://github.com/user-attachments/assets/980a83e1-dfce-4902-bb85-e44d47af9088" />
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
twine upload --repository testpypi dist/* --verbose
```

```output
Uploading distributions to https://test.pypi.org/legacy/
INFO     dist/greet_me-0.1.1-py3-none-any.whl (0.9 KB)                                                                                                                                                                     
INFO     dist/greet_me-0.1.1.tar.gz (4.9 KB)                                                                                                                                                                               
INFO     username set by command options                                                                                                                                                                                   
INFO     Querying keyring for password                                                                                                                                                                                     
INFO     No keyring backend found                                                                                                                                                                                          
Enter your API token: 
INFO     username: __token__                                                                                                                                                                                               
INFO     password: <hidden>                                                                                                                                                                                                
Uploading greet_me-0.1.1-py3-none-any.whl
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.6/2.6 kB • 00:00 • ?
INFO     Response from https://test.pypi.org/legacy/:                                                                                                                                                                      
         400 Bad Request                                                                                                                                                                                                   
INFO     <html>                                                                                                                                                                                                            
          <head>                                                                                                                                                                                                           
           <title>400 The name 'greet-me' is too similar to an existing project. See https://test.pypi.org/help/#project-name for more information.</title>                                                                
          </head>                                                                                                                                                                                                          
          <body>                                                                                                                                                                                                           
           <h1>400 The name 'greet-me' is too similar to an existing project. See https://test.pypi.org/help/#project-name for more information.</h1>                                                                      
           The server could not comply with the request since it is either malformed or otherwise incorrect.<br/><br/>                                                                                                     
         The name &#x27;greet-me&#x27; is too similar to an existing project. See https://test.pypi.org/help/#project-name for more information.                                                                           
                                                                                                                                                                                                                           
                                                                                                                                                                                                                           
          </body>                                                                                                                                                                                                          
         </html>                                                                                                                                                                                                           
ERROR    HTTPError: 400 Bad Request from https://test.pypi.org/legacy/                                                                                                                                                     
         Bad Request                   
```

To fix this, 
- rename your project (e.g. from `greet_me` to `po_greet_me`).
- Update your `pyproject.toml` accordingly.
- Rebuild and upload the package.

```toml
[tool.hatch.build.targets.wheel]
packages = ["my_package"]
```

```bash
# 1. (Recommended) Remove the old build directory
rm -rf dist

# 2. Re-build your package with the new name
python -m build

# 3. Upload the new version to TestPyPI
twine upload --repository testpypi dist/*
```

## Step 4: Test your package

Install your package from TestPyPI via this command : 

```bash
pip install --index-url https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple po-greet-me==0.1.1
```

```output
Looking in indexes: https://test.pypi.org/simple/, https://pypi.org/simple
Collecting po-greet-me==0.1.1
  Downloading https://test-files.pythonhosted.org/packages/52/85/dd6ebf4ee0a6ff76699a4c4f134059e6615b75c50e30cd40cd424370b81e/po_greet_me-0.1.1-py3-none-any.whl.metadata (137 bytes)
Downloading https://test-files.pythonhosted.org/packages/52/85/dd6ebf4ee0a6ff76699a4c4f134059e6615b75c50e30cd40cd424370b81e/po_greet_me-0.1.1-py3-none-any.whl (815 bytes)
Installing collected packages: po-greet-me
Successfully installed po-greet-me-0.1.1
```

Then create a test script : `test_package.py`:

```python
from my_package import happy, sad

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
