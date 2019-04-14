---
layout: post
title: Unix like Python Development Environment on Windows 7
tags: [unix, development, windows7, environment, python, anaconda, cmder]
image: /img/posts/2019-02-12-unix-python-dev-windows7/preview.jpg
---

I do most of my development at the office under Linux. I wanted to recreate that evironment and have access to some of the same tools at home where my operating system in Windows 7.

Goals
=====

My goals were:

* Manage versions of Python and various packages in different environments.
* Use Sphinx to build documentation.
* Use pytest for testing.
* Use a Unix like shell and commands for day to day tasks.
* Have Sublime Text pick up the python version/environment of my choice.
* Use pycodestyle for Sublime Text linting.
* Launch a shell in the environment of my choice.
* Launch gitk to see repository state.

Method
======

To do this I used Anaconda for package and Python version management, cmder for a Unix like shell and git for windows for gitk access. Here are the steps I took:

Install Anaconda
----------------

Install [Anaconda](https://www.anaconda.com/distribution/). I didn't add it to my PATH variable or register Anaconda's Python to keep things isolated:

[![Path options](/img/posts/2019-02-12-unix-python-dev-windows7/anaconda-no-system.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/anaconda-no-system.jpg)

[Miniconda](https://www.anaconda.com/distribution/) is a lighter alternative
(~70MB vs ~300MB) but you lose the convenient GUI.


Create a new Anaconda Environment
---------------------------------

For now I'm using Python 2 so I called mine `py2`. Creating a new environment made sure it was clean and would only include the things I needed. While testing I was having issues with Sphinx picking up the wrong Python version if I didn't create a new environment.

[![Creating a new environment](/img/posts/2019-02-12-unix-python-dev-windows7/anaconda-py2-env.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/anaconda-py2-env.jpg)

This is also possible on the command line with:

```
conda create --name py2 python=2.7
```

Add required packages to the environment
----------------------------------------

I added:

* sphinx
* pycodestyle
* m2-base
* git
* sphinx_rtd_theme
* pytest

[![Adding packages](/img/posts/2019-02-12-unix-python-dev-windows7/anaconda-packages.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/anaconda-packages.jpg)

This is also possible on the command line with:

```
conda install --name py2 sphinx pycodestyle m2-base git sphinx_rtd_theme pytest
```

Install cmder
-------------

[cmder](https://cmder.net/) is a standalone executable. I created a `cmder-mini` folder along side my cloned repositories and extracted the contents into there.

Configure cmder to launch into the py2 environment
--------------------------------------------------

I created a new task by cloning the default `{cmd::Cmder}` task and editing the commands to:

```
cmd /k ""%ConEmuDir%\..\init.bat"" & C:\Users\Andy\Anaconda3\Scripts\activate.bat C:\Users\Andy\Anaconda3 & -new_console:d:C:\dev conda activate py2
```

Which activates the py2 conda environment and changes directory into the folder where I keep my cloned repositories (`C:\dev`).

[![Creating a new cmder task](/img/posts/2019-02-12-unix-python-dev-windows7/cmder-settings.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/cmder-settings.jpg)

I also set it up to be the default task in the general settings:

[![Setting the default task](/img/posts/2019-02-12-unix-python-dev-windows7/cmder-settings-startup.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/cmder-settings-startup.jpg)

Add aliases to cmder
--------------------

[The cmder homepage](https://cmder.net/) mentions creating aliases but after running alias `ll=ls -l $*` I wasn't getting colours from ls coming through.

Instead I altered the alias file (`C:\dev\cmder_mini\config\user_aliases.cmd` in my case) to add a more explicit `ll` alias. The file now contains:

```
;= @echo off
;= rem Call DOSKEY and use this file as the macrofile
;= %SystemRoot%\system32\doskey /listsize=1000 /macrofile=%0%
;= rem In batch mode, jump to the end of the file
;= goto:eof
;= Add aliases below here
e.=explorer .
gl=git log --oneline --all --graph --decorate  $*
ls=ls --show-control-chars -F --color $*
ll=ls -l --show-control-chars -F --color $*
pwd=cd
clear=cls
history=cat "%CMDER_ROOT%\config\.history"
unalias=alias /d $1
vi=vim $*
cmderr=cd /d "%CMDER_ROOT%"
```

Create a launcher to launch Sublime Text in the py2 environment
---------------------------------------------------------------

This is the content of the `sublimetext_py2.bat` file I have on the desktop:

```
CALL C:\Users\Andy\Anaconda3\Scripts\activate.bat C:\Users\Andy\Anaconda3\envs\py2
start "" "C:\Program Files\Sublime Text 3\sublime_text.exe
```

A [superuser.com post](https://superuser.com/questions/192550/why-wont-cmd-exit-after-execution-of-batch-file) was helpful as a previous version of the launcher would leave a `cmd.exe` window open behind Sublime Text.

Install Git for Windows
-----------------------

[Git for Windows](https://git-scm.com/downloads) contains gitk. A quick search didn't reveal an easy way just to install gitk so unfortunately  there’s a little duplication as git is managed by Anaconda.

I initially wanted to keep things clean and make no additions to my PATH, however, this meant a cmder shell couldn't find gitk so I left the minimal PATH additions in place when setting it up:

[![Creating a new cmder task](/img/posts/2019-02-12-unix-python-dev-windows7/git-windows-path.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/git-windows-path.jpg)

Git Setup
---------

You may need to run the following to get you setup and provide password convenience:
```
git config --global user.email "your@email.com"
git config --global user.name "Your Name"
git config --global credential.helper wincred
```

[The github docs](https://help.github.com/en/articles/caching-your-github-password-in-git) were helpful here.

Conclusions
===========

The [Conda task docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html) have lots of useful information and examples.

I was getting what looked like Python execution errors if I ran conda commands in the py2 environment:

[![Conda Python errors](/img/posts/2019-02-12-unix-python-dev-windows7/conda-python-errors.jpg)](/img/posts/2019-02-12-unix-python-dev-windows7/conda-python-errors.jpg)

I believe this is because I installed Anaconda 3 which uses Python 3 by default so it's calling Python 2 but expecting it to be Python 3. I didn't get these errors if I ran the conda commands in the `base` env.

It would be interesting to see how usable a VM running Ubuntu would be as alternative to this setup.

Pip also installs packages and can be used as normal inside a conda environment (as per [the docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html#installing-non-conda-packages)).