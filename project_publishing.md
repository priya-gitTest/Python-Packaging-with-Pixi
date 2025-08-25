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

- Learn the usage for tools like build and twine
- How to upload the Python Package to repositories like TestPyPi
- How to use the uploaded package.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction
Once we have created our project, defined all the necessary metadata in the toml file, its time to publish our project. Let see the tools and steps we need to acheive this.

We need to install the following tools i.e. `build` and `twine`

##  Create your build

`build` :A tool to read the `pyproject.toml` file and build the package files

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


 ## Create an account on TestPyPI
     
     Visit this [URL](https://test.pypi.org/account/register/) and crete an account to generate the API keys, to be able to upload your package to TestPyPI in the next step.
     Once you create your account, you can visit this [link](https://test.pypi.org/manage/account/token/) to generate the API key. Please copy the same in a notepad and paste it when prompted for it in the next step below.
     
<img width="1726" height="625" alt="image" src="https://github.com/user-attachments/assets/0c27a806-8fa2-469a-8b5c-fbf73c47e5e6" />
     

## Upload your build
`twine` :A tool for securely uploading packages to PyPI and TestPyPI.
   ```bash
   pip install build twine

   twine upload --repository testpypi dist/*
   ```
  You'll be prompted to enter your TestPyPI username and password. It's recommended to use an API token instead of      your password. When prompted for your password, paste the token in.

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

  That's it! After the upload is successful, your package will be available on TestPyPI. E.g. : https://test.pypi.org/project/po-greet-me/0.1.1/
  
<img width="1619" height="854" alt="image" src="https://github.com/user-attachments/assets/980a83e1-dfce-4902-bb85-e44d47af9088" />

  It is possible that the name of your project already exists or is simialr to an existing project. In that case you may end up in an error like this : 
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
To fix this, rename you project e.g. to `po_greet_me` , and add the following in `pyproject.toml` file.
and try the steps below to upload it again.
```toml
[tool.hatch.build.targets.wheel]
packages = ["src/po_greet_me"]
```
```bash
# 1. (Recommended) Remove the old build directory
rm -rf dist

# 2. Re-build your package with the new name
python -m build

# 3. Upload the new version to TestPyPI
twine upload --repository testpypi dist/*
```

## Test your package
Install your package via this command : 
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
Create a Python file named test_package.py

```python
from my_package import happy, sad

print(happy.greet_happy())
```

```bash
python test_package.py 
```
```output
Yay! happy day! 😀
```

::::::::::::::::::::::::::::::::::::: keypoints
- Fill all the metadata and give your project a unique name
- Build your Project
- Create a TestPyPI account and generate the API token
- Upload your package via twine to TestPyPI
- Check your package via pip install
::::::::::::::::::::::::::::::::::::::::::::::::
