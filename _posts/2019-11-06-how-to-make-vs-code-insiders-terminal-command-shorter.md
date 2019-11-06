---
layout: post
title: How to make VS code insiders terminal command shorter
tags:
  - OSX
  - Windows
comments: true
---

![_config.yml]({{ site.baseurl }}/images/vscode.png)
Since from last year, I slowly switch most of my daily development utilities from stable to beta version to enjoy the latest features and earlier bug fixes. So far, the experience is not that bad comparing to use stable version. Most of the utilities are able to install side by side without too much impact on my daily usage except `Visual Studio Code Insiders`. In this short blog post, I'll show you my way to shorten the terminal command on both Windows and OSX.  

Before you start to tweak the alias, you first need to make sure install code-insiders command in PATH. Start Visual Studio Insiders, Open `Command Palette` from view menu

![_config.yml]({{ site.baseurl }}/images/vscodeinsiders/command-palette.jpg)

Type `Insiders` in the command palette search bar, and choose `Shell Command : Install 'code-insiders' command in PATH`

![_config.yml]({{ site.baseurl }}/images/vscodeinsiders/install-insiders-command.jpg)

Once the above is done, open terminal (OSX) / Dos prompt (Windows), type `code-insiders`, this will launch Visual Studio Code Insiders from terminal.

The next step is to change `code-insiders` to `c`. 

## Windows 

1. Create a folder (e.g. tools under c drive) and add it to your PATH environment variable, so you can access the command from prompt (Dos/Powershell).
2. Download [32 bit]({{ site.baseurl }}/images/vscodeinsiders/32bit/c.cmd)/[64 bit]({{ site.baseurl }}/images/vscodeinsiders/64bit/c.cmd) version batch file and save into the the new folder you created in step 1.
3. Open a new Dos/Powershell prompt, type `c`, and it will launch Visual Studio Code Insiders.

## OSX
1. Use your preferable editor to open `.bash_profile` file.
2. Add an alias `alias c='code-insiders'` in your alias section, if you don't have separate alias section, just add it to the end. 
3. Save changes, go back to terminal type `source ~/.bash_profile` to reload your updated bash profile. 
4. Type `c` in terminal this time, it will launch Visual Studio Code Insiders. 

![_config.yml]({{ site.baseurl }}/images/vscodeinsiders/osx-alias.jpg)

Happy Coding! 😇
