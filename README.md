# MSYS2-Setup-Guide
An installation/configuration guide to help setting up MSYS2 on Microsoft Windows and use it in Visual Studio Code

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

MSYS2 is an awesome command-line environment for the Microsoft Windows operating system, providing various terminal shells (e.g., `bash`, `zsh`, etc.) along with important tools (e.g., `gcc`, `git`, etc.). It is bundled with its own package manager and software repository called `pacman`, providing access to the latest binary versions of many essential development tools.

Although the benefits of this software are significant, the setup procedure – especially configuring it with Visual Studio Code – might be a bit tricky. Additionally, there are some points in the correct installation and usage which, if not handled properly, might cause the program to crash.

---

## Prerequisites

Before installing MSYS2, it is generally recommended to perform some actions to avoid potential problems.

1. Run the Registry Editor (Press <kbd>⊞ Win</kbd> + <kbd>R</kbd> and type in `regedit`).
2. Navigate to `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor`.
3. Delete the `Autorun` key if it is present.

This ensures that the Windows Command Prompt will work properly and will not cause further issues.

---

## Installation

To install MSYS2 on the Microsoft Windows operating system, please follow the steps below:
1. Go to the [MSYS2 releases page](https://github.com/msys2/msys2-installer/releases) and download the latest **.exe** version of the installer (the `msys2-x86_64-release_date.exe` file).
2. Run the downloaded installer file (you might want to run it as an Administrator).
3. Click on Next.
4. Choose your preferred installation path and click on Next. (Note that the path must not contain any spaces.)
5. Choose the Start Menu shortcuts folder name and click on Next.
6. Let the installer extract the files.
7. Check the `Run MSYS2 64bit now.` option and click on Finish.

An MSYS2 instance will pop up. Please follow the instructions below to complete the MSYS2 installation procedure:
1. Run the command `pacman -Syu` and enter Y if prompted. This will update the package repository data for MSYS2.
2. Run the command `pacman -Su` and enter Y if prompted. This will update all installed packages on MSYS2.
3. (Optional) If you want to install the GNU Compiler Collection (GCC) or Git, run the command `pacman -S --needed base-devel mingw-w64-x86_64-toolchain git`.
4. (Optional) Search for `Edit the system environment variables` in the Start Menu and open it, then click on `Environment Variables`. Under `User variables for your_username`, select Path and click on `Edit`, then `Add`, and enter `C:\msys64\mingw64\bin`. (Replace `C:\msys64` with your MSYS2 installation location.) This will allow you to access MSYS2 installed packages from other terminals.

---

## Setting Up MSYS2 on Visual Studio Code

You may use Visual Studio Code (VS Code) as your preferred IDE and want to use MSYS2 as the default terminal. In order to add MSYS2 as a terminal option and set it as the default terminal, follow the steps below:

1. In Visual Studio Code, go to `File -> Preferences -> Settings` (or use the `Ctrl + ,` keyboard shortcut) and click on "Open Settings (JSON)" (or look for the `terminal.integrated.profiles.windows` setting and click on "Edit in settings.json").
2. Add the following lines inside the `settings.json` file:
   ```json
   "terminal.integrated.profiles.windows": {
       "Bash": {
           "path": "C:\\msys64\\usr\\bin\\bash.exe",
           "args": ["--login", "-i"],
           "env": {
               "MSYSTEM": "MINGW64",
               "CHERE_INVOKING": "1",
               "MSYS2_PATH_TYPE": "inherit"
           }
       }
   },
   "terminal.integrated.defaultProfile.windows": "Bash",
   "git.path": "C:\\msys64\\usr\\bin\\git.exe"
   ```
3. Restart Visual Studio Code.
4. Go to `Terminal -> New Terminal` (or use the `` Ctrl + Shift + ` `` keyboard shortcut).
5. The loaded terminal will be an MSYS2 terminal (MinGW64).

### Oh-My-Zsh `\` Problem

If you use Oh-My-Zsh and see a `\` at the beginning of your terminal lines, there is a fix for it as follows:
1. Add the following inside the `settings.json` file:
   ```json
   "terminal.integrated.windowsEnableConpty": false
   ```
2. Restart Visual Studio Code.

---
