---
layout: post
title: Setting Up Your Python Environment
description: "... on a Windows system."
modified: 2020-05-24
tags: [python]
---

These days there are countless ways to set up Python on your system. The method that would work best for you is likely available but with so many available options, how would you go about finding the right one for you?

If you are like me and develop code in multiple languages and would like to have control over what is installed (installing only what you need), without having to readjust to different development environments as you switch languages, read on.

The steps below are described for the current versions of Python (3.8).

# Download Python

Head to [python.org](https://python.org) and download the latest version.

Then choose the `Windows x86-64 executable installer`.

In the options, ensure that you have `pip` installed. By selecting "for all users", Python will be installed in `Program Files`.
<figure>
  <img src="/images/python-setup-optional-features.png">
</figure>

# Download Visual Studio Code

Before using Visual Studio Code, I was a big fan of Microsoft Visual Studio's Python Tools. Initially, working with Visual Studio Code was causing me various difficulties but the current versions provide for a smooth development process.


After having given up on Visual Studio Code, [this](
https://kenreitz.org/essays/why-you-should-use-vs-code-if-youre-a-python-developer
) article convinced me to give it another try.


Before switching to VSCode, I was using Visual Studio with the Python Extensions. However, I was not a fan of using the workflow for development of Windows projects for Python. In Python everything is determined by the project structure and you only want to specify additional stuff.

Additionally, you get:

Great integration with Jupyter notebooks.

This year's MSBuild conference also announced all the cool things they are doing with Visual Studio Code (which will be embedded into GitHub to allow you to code without having to set it up on your computer, etc.)

Additionally, VSCode has developed a rich set of toolboxes for data processing in Python, which will make your job much easier.

# Setting up a Virtual Environment

This step helps you keep the dependencies for your projects separate.

Otherwise, all Python packages that you install are going to be in Lib\site-packages.

This will work fine until the time when you have to give your project to someone else and you will have no idea which of  the installed packages in your Python directory it depends on.

## Choosing a home for your virtual environment

You can either place the virtual environment in the directory of the project that uses the virtual environment or in a directory of virtual environments. 

I prefer the latter option because:
Multiple projects can use the same virtual environment
When searching for files in the folder of your project, you are likely not to want to search for code that came with your python installation or code that you installed using the Python packages. Instead, you would rather focus on the code that you wrote.


## Setting up your virtual environment

After you install Python, typing "python" in the command prompt would start the Python interactive prompt for the version that you installed if the directory in which the executable is located has been added to your Path environment variable in Windows. You can check the contents of your Environment Variable from This PC > Properties > Advanced System Settings.

If Python is not a part of it, you will have to use the full path to the executable to create your virtual environment.

The command to use is:

```
python -m venv name_of_your_virtual_environment
```

After you run this in the command prompt, Python will create a directory containing the virtual environment.

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

If you prefer to keep your virtual environments at a custom location in your home directory, you may also set `Venv Folders`. Here you need to list only the folder names.

After this step, you need to reboot Visual Studio Code.


To select your environment, press `Ctrl + Shift + P` and select yours from the list. Some examples of that are shown [here](https://code.visualstudio.com/docs/python/environments).

Open Visual Studio press open the directory where you wish to work on your Python project.


Press Ctrl + Shift + P to select the terminal.

## Creating an integrated terminal

Press `Ctrl + Shift + P` : `Python: Create Terminal`

This will create a terminal which is specific to your virtual environment.

For example, typing python will start the Python shell.

Note that you may need to run ```Set-ExecutionPolicy RemoteSigned``` in PowerShell to allow the virtual environment activation to work. More info is available [here](
  https://github.com/Microsoft/vscode-python/issues/2559
).

## Installing packages

With the terminal running, run ```pip install package_name```. This will install ```package_name``` into your virtual environment.

## requirements.txt

You've set up your project nicely but what if you wanted to create an easy way to install all the dependencies that are needed to run your project?

You can use `pip freeze` to accomplish this goal:

```
pip freeze > requirements.txt
```

Running this from your activated terminal will write the file to your current directory.

To install the necessary packages from a `requirements.txt` that someone provided, use:

```
pip install -r requirements.txt
```
