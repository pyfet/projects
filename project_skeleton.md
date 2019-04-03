This will be where you start learning how to set up a good project “skeleton” directory.
This skeleton directory will have all the basics you need to get a new project up and running.
It will have your project layout, automated tests, modules, and install scripts.
When you go to make a new project, just copy this directory to a new name and edit the files to get started.
macOS/Linux Setup
Before you can begin this exercise you need to install some software for Python by using a tool called pip3.6 (or just pip) to install new modules. The pip3.6 command should be included with your python3.6 installation. You’ll want to verify this using this command:

    $ pip3.6 list
    pip (9.0.1)
    setuptools (28.8.0)

You can ignore any deprecation warning if you see it. You may also see other tools installed, but the base should be pip and setuptools. Once you’ve verified this you can then install virtualenv:

    $ sudo pip3.6 install virtualenv
    Password:
    Collecting virtualenv
      Downloading virtualenv–15.1.0–py2.py3–none–any.whl (1.8MB)
        100% ||||||||||||||||||||||||||||||||| 1.8MB 1.1MB/s
    Installing collected packages: virtualenv
    Successfully installed virtualenv–15.1.0

This is for Linux or macOS systems. If you’re on Linux/macOS, you’ll want to run the following command to make sure you use the correct virtualenv:

    $ whereis virtualenv
    /Library/Frameworks/Python.framework/Versions/3.6/bin/virtualenv
    You should see something like the above on macOS, but Linux will be variable. On Linux you might have an actual virtualenv3.6 command, or you may be better off installing a package for it from your package management system.
    Once you’ve installed virtualenv you can use it to create a “fake” Python installation, which makes it easier to manage versions of your packages for different projects. First, run this command, and I’ll explain what it’s doing:
    $ mkdir ~/.venvs
    $ virtualenv ––system–site–packages ~/.venvs/lpthw
    $ . ~/.venvs/lpthw/bin/activate
    (lpthw) $

Here’s what’s going on line by line:
1. You create a directory called .venvs in your HOME ~/ to store all your virtual environments.
2. You run virtualenv and tell it to include the system site packages (--system-site-packages), then instruct it to build the virtualenv in ~/.venvs/lpthw.
3. You then “source” the lpthw virtual environment by using the . operator in bash, followed by the ~/.venvs/lpthw/bin/activate script.
4. Finally, your prompt changes to include (lpthw), so you know that you’re using that virtual environment.

Now you can see where things are installed:

    (lpthw) $ which python
    /Users/zedshaw/.venvs/lpthw/bin/python
    (lpthw) $ python
    Python 3.6.0rc2 (v3.6.0rc2:800a67f7806d, Dec 16 2016, 14:12:21)
    [GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> quit()
    (lpthw) $

You can see that the python that gets run is installed in the /Users/zedshaw/.venvs/lpthw/bin/ python directory instead of the original location. This also solves the problem of having to type python3.6 since it installs both:

    $ which python3.6
    /Users/zedshaw/.venvs/lpthw/bin/python3.6
    (lpthw) $

You’ll find the same thing for virtualenv and pip commands. The final step in this setup is to install nose, a testing framework we’ll use in this exercise:

    $ pip install nose
    Collecting nose
      Downloading nose–1.3.7–py3–none–any.whl (154kB)
        100% |||||||||||||||||||||||||||||||||| 163kB 3.2MB/s
    Installing collected packages: nose
    Successfully installed nose–1.3.7
    (lpthw) $

Windows 10 Setup
The Windows 10 install is a little simpler than on Linux or macOS, but only if you have one version of Python installed. If you have both Python 3.6 and Python 2.7 installed then you are on your own as it is much too difficult to manage multiple installations. If you have followed the book so far and have only Python 3.6, then here’s what you do. First, change to your home directory and confirm you’re running the right version of python:

    > cd ~
    > python
    Python 3.6.0 (v3.6.0:41df79263a11, Dec 23 2016, 08:06:12)
        [MSC v.1900 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>> quit()
    Then you’ll want to run pip to confirm you have a basic install:
    > pip list
    pip (9.0.1)
    setuptools (28.8.0)

You can safely ignore any deprecation warning, and it’s alright if you have other packages installed. Next, you’ll install virtualenv for setting up simple virtual environments for the rest of the book:

    > pip install virtualenv
    Collecting virtualenv
      Using cached virtualenv–15.1.0–py2.py3–none–any.whl
    Installing collected packages: virtualenv
    Successfully installed virtualenv–15.1.0

Once you have virtualenv installed you’ll need to make a .venvs directory and fill it with a virtual environment:

    > mkdir .venvs
    > virtualenv ––system–site–packages .venvs/lpthw

Using base prefix
        'c:\\users\\zedsh\\appdata\\local\\programs\\python\\python36'
    New python executable in
        C:\Users\zedshaw\.venvs\lpthw\Scripts\python.exe
    Installing setuptools, pip, wheel...done.

Those two commands create a .venvs folder for storing different virtual environments and then create your first one named lpthw. A virtual environment (virtualenv) is a “fake” place to install software so that you can have different versions of different packages for each project you’re working on. Once you have the virtualenv set up you need to activate it:

    > .\.venvs\lpthw\Scripts\activate

That will run the activate script for PowerShell, which configures the lpthw virtualenv for your current shell. Every time you want to use your software for the book you’ll run this command. You’ll notice in our next command that there is now a (lpthw) added to the PowerShell prompt showing you which virtualenv you’re using. Finally, you just need to install nose for running tests later:

    (lpthw) > pip install nose
    Collecting nose
      Downloading nose–1.3.7–py3–none–any.whl (154kB)
        100% |||||||||||||||||||||||||||||||||| 163kB 1.2MB/s
    Installing collected packages: nose
    Successfully installed nose–1.3.7
    (lpthw) >

You’ll see that this installs nose, except pip will install it into your .venvs\lpthw virtual environment instead of the main system packages directory. This lets you install conflicting versions of Python packages for each project you work on without infecting your main system configuration.
Creating the Skeleton Project Directory
First, create the structure of your skeleton directory with these commands:

    $ mkdir projects
    $ cd projects/
    $ mkdir skeleton
    $ cd skeleton
    $ mkdir bin NAME tests docs

I use a directory named projects to store all the various things I’m working on. Inside that directory I have my skeleton directory that I put the basis of my projects into. The directory NAME will be renamed to whatever you are calling your project’s main module when you use the skeleton.
Next, we need to set up some initial files. Here’s how you do that on Linux/macOS:

    $ touch NAME/__init__.py
    $ touch tests/__init__.py

Here’s the same thing on Windows PowerShell:

    $ new–item –type file NAME/__init__.py
    $ new–item –type file tests/__init__.py

That creates an empty Python module directory we can put our code in. Then we need to create a setup.py file we can use to install our project later if we want:
