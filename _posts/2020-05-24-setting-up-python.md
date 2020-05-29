---
layout: post
title: Setting Up Your Python Environment
description: "... on a Windows system."
modified: 2020-05-24
tags: [python]
---

With so many ways to set up Python on your system, how would you choose the right one for you?

If you
1. develop code in multiple languages but would rather use a single environment
2. like to control what is installed (installing only what you need)
3. enjoy the code editor experience but also require customization
like I do, this post is for you.

The steps below apply to Python 3.8 and Visual Studio Code (VS Code) 1.44.2.

# Download Python

Head to [python.org](https://python.org) and download the latest version.

Then choose the `Windows x86-64 executable installer`.

In the options, ensure that you have `pip` installed. Select "for all users" to install Python in `Program Files`.
<figure>
  <img src="/images/python-setup-optional-features.png">
</figure>

# Download Visual Studio Code

Before using Visual Studio Code, I was a big fan of Microsoft Visual Studio's Python Tools... with the exception of the "creating a project" part. I would much rather define the project in terms of its directory structure.

Initially, Visual Studio Code was causing me various difficulties but the current versions provide for a smooth development experience with little taking your fingers off the keyboard.


After having given up on Visual Studio Code, [this article](
https://kenreitz.org/essays/why-you-should-use-vs-code-if-youre-a-python-developer
) convinced me to give it another try.

Additionally, you get great integration with Jupyter.

# Setting up a Virtual Environment

This step helps you separate project dependencies.

In the alternative, you will lose track of the Python packages (and their versions) needed for a specific project and make other contributors to your projects suffer inordinately.

## Choosing a home for your virtual environment

You can either place the virtual environment in the directory of the project that uses the virtual environment or in a directory of virtual environments. 

I prefer the latter option because:
1. Multiple projects can use the same virtual environment
2. You likely want matches from your own code when searching your project directory (and not matches from your Python virtual environment)

## Setting up your virtual environment

If your Python installation is on your Windows path, typing `python` in the Command Prompt would start the Python shell. (You can view your path from your `Environment Variables...` from `This PC` > `Properties` > `Advanced System Settings`.)

If Python is not on your path, you will have to use the full path to the executable to create your virtual environment.

The command to use is:

```
python -m venv path_to_your_virtual_environment
```

Python will place the virtual environment files where you specified.

## Activating a virtual environment

To allow Visual Studio code to find your virtual environments, you need to specify their location.

Press `Ctrl + ,` to open settings and type `venv`.

You will see two options, `Venv Folders` and `Venv Path`.

<figure>
  <img src="/images/vscode-python-venv-settings.png">
</figure>

To specify a directory containing the virtual environments for your project, use `Venv Path`:

```json
"python.venvPath": "X:\\Python\\venv"
```

If you prefer to keep your virtual environments at a custom location in your home directory, you may also set `Venv Folders`. There you need to list only the folder names.

After this step, you need to reboot Visual Studio Code.


Press `Ctrl + Shift + P` to select your virtual environment from the list. Some examples are shown [here](https://code.visualstudio.com/docs/python/environments).

## Creating an integrated terminal

Press `Ctrl + Shift + P` : `Python: Create Terminal`

This will create a terminal which is specific to your virtual environment.

For example, typing `python` will start the Python shell for your virtual environment.

Note that you may need to run ```Set-ExecutionPolicy RemoteSigned``` in PowerShell to allow the virtual environment activation to work. More info is available [here](
  https://github.com/Microsoft/vscode-python/issues/2559
).

## Installing packages

With the terminal running, run ```pip install package_name```. This will install ```package_name``` into your virtual environment.

## requirements.txt

Having installed all the packages you need, how could you let a contributor easily replicate your setup?

You can use `pip freeze` to accomplish this goal:

```
pip freeze > requirements.txt
```

Running this from your activated terminal will write the file `requirements.txt` to your project directory.

To install the necessary packages from a `requirements.txt`, use:

```
pip install -r requirements.txt
```
