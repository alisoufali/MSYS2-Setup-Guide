# MSYS2-Setup-Guide
An installation/configuration guide to help setting up MSYS2 on microsoft windows and use it in Visual Studio Code

---

## Table of contents
- [MSYS2-Setup-Guide](#msys2-setup-guide)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Setting-Up MSYS2 on Visual Studio Code](#setting-up-msys2-on-visual-studio-code)

---

## Introduction

MSYS2 is a terminal software for microsoft windows operating system providing us different terminal shells (e.g., bash, zsh and etc.) alongside with important tools (e.g., gcc, git and etc.). It is bundeled with its own package manager and software repository letting us have access to the latest binary versions of many development necessity tools.
Although the benefits of this software are very good, the setting-up procedure, specially to configure it on Visual Studio Code might be tricky. Also there are some points in correct installation and usage which if not handled properly it might cause the program to crash. 

---

## Prerequisites

Before installing MSYS2 it is good to perform some actions to avoid further problems. 

1. Run registry editor (ctrl+r and type in regedit).
2. Go to the address `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor`.
3. Delete `Autorun` key if it is present there.

In this way we make sure that windows command prompt will work properly and will not cause further problems.

---

## Installation

To install MSYS2 on microsoft windows operating system please follow the steps below:
1. Go to the [MSYS2 releases page](https://github.com/msys2/msys2-installer/releases) and download the latest .exe version of the installer (the `msys2-x86_64-release_date.exe` file).
2. Run the downloaded installer file (You might want to run it as an adminstrator.)
3. Click on Next.
4. Choose your favorite path of installation and click on Next. (Note that the path must be without any spaces)
5. Choose the start menu shortcuts folder name and click on Next.
6. Let the installer to extract file.
7. Check the `Run MSYS2 64bit now.` and click on Finish.

A MSYS2 instance will pop up. Please follow the below instructions to complete the MSYS2 installation procedure:
1. Run the command `pacman -Syu` and enter Y if a confirm is asked. This will update the package repository data for MSYS2.
2. Run the command `pacman -Su` and enter Y if a confirm is asked. This will update all installed packages on MSYS2.
3. (Optional) You may want to have GNU Compiler Collection (GCC) or GIT. To have them installed please run the command `pacman -S --needed base-devel mingw-w64-x86_64-toolchain git`
4. (Optional) Search for `Edit the system environment variables` in the start menu and open it, then click on `Environment Variables`. From the `User variables for your_username`, select Path and click on `Edit` then `Add` and enter `C:\msys64\mingw64\bin`. (You may replace `C:\msys64` with your main installation location of MSYS2). After this you will have access to MSYS2 installed packages from other terminals.

---

## Setting-Up MSYS2 on Visual Studio Code

You may use Visual Studio Code (VSCODE) as your favorite IDE and want to use MSYS2 as the default terminal. In order to add MSYS2 as an available terminal and set it as default terminal please follow the steps below:
1. In Visual Studio Code go to `File -> Preferences -> Settings` (or use `ctrl + ,` keyboard shortcut) and click on the Open Settings (JSON) (Or look for `terminal.integrated.profiles.windows` setting and click on `Edit in settings.json`)
2. Add the following lines inside the settings.json file.
   ```json
    "terminal.integrated.profiles.windows": {
        "BASH": {
            "path": "C:\\msys64\\usr\\bin\\bash.exe",
            "args": [ "--login", "-i"],
            "env": { "MSYSTEM": "MINGW64", "CHERE_INVOKING": "1", "MSYS2_PATH_TYPE": "inherit"}
        }
    },
    "terminal.integrated.defaultProfile.windows": "BASH",
    "git.path": "C:\\msys64\\usr\\bin\\git.exe"
    ```
3. Restart the Visual Studio Code.
4. Go to `Terminal -> New Terminal` (or use ``ctrl + shift + ` `` keyboard shortcut)
5. The loaded terminal will be an MSYS2 terminal (MINGW64)

---

