# Cumulative for the pip and install pip

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:
- Describe what pip is
- Download packages with pip
- upgrade packages with pip
- remove packages with pip


</details>


<details><summary>Description</summary>

# Introduction
Python comes with a package management system called "Pip Installs Packages," abbreviated as pip. By default, pip tries to download third-party packages from PyPI, the main repository for third-party Python packages. The code stored in this repository ranges from people's experiments they wanted to share to high-end, enterprise-grade, production-ready software.

When you download packages with pip, they will be saved in your Python library. Still, common practice is to create a "virtual environment" for any project that requires using third-party libraries. This virtual environment has a copy of the interpreter and Python library used to create it, and any pip installs are redirected to the virtual environment instead of the global Python install when the environment is "activated." The command `py -m venv {environment-name}` will create your virtual environment. When it is created, you can execute whatever "activate" script is appropriate for your OS, and your pip install will be redirected to the virtual environment.

</details>
<details><summary>Real World Application</summary>

# Real World Application for Pip
The world of software is ever evolving, but even new and innovative ideas tend to need resources created by those who came before us. When building an application, there will almost always be someone who has had a similar need as you and has already built a solution to the problem. These solutions typically end up as packages stored in PyPI, free for you to implement in your own project. The benefit of this system is that you can focus on your application's specific logic and features, utilizing third-party packages of software that are ready to go and that have been developed by someone else. Some common use cases for using third-party packages:
- building web servers
- creating and executing tests
- creating more complex logs
- performing complex mathematical computations
- managing large data sets

</details>
<details><summary>Implementation</summary>

# Implementation

## Acquiring Pip
If you downloaded Python from the main Python website or from any other major Python distributor, then you should already have pip. An easy way to check is to run either of the following commands:
```cli
pip --version
```
```cli
py -m pip --version
```
If the output is your version of pip, then you are good to go. If you don't have it for some reason, you have a few options. First, try running the "ensurepip" module:
```cli
py -m ensurepip --default-pip
```
In most cases, this should be enough, but if that also fails, you can download a module called "get-pip.py" from [this](https://packaging.python.org/en/latest/tutorials/installing-packages/) packaging tutorial.

If all these options fail, then uninstalling and reinstalling Python from its main website will probably be your best fix.

## Installing Packages
When installing packages, you have a few options for how you perform the download. The simplest way is just to use the install command:
```cli
pip install {package-name}
```
Pip will try to install the most up-to-date version of the package. If you know you need a specific version of the package, you can specify the version:
```cli
pip install {package-name}=={version.number}
```
You can also specify a lower and upper bound for the version, and pip will attempt to grab the most up-to-date version of your specified package that meets the requirements. There are two approaches to this option, as shown below. The first sets a hard upper and lower bound for the version. The second option sets a "compatible" version pip checks against, and it will attempt to download the most up-to-date version of the package that is compatible with your chosen version:
```cli
pip install "{package-name}>={lower.bound},<={upper.bound}"
```
```cli
pip install {package-name}~={version.you.want.compatibility.with}
```
To clarify the example, imagine there are four versions of the package:
- 0.1.1
- 0.1.2
- 0.2.1
- 0.3.1

If you specify `pip install package~=0.1`, pip will try to download version 0.1.2, since it is not a major change from your indicated version.

## Upgrade Packages
To upgrade a package, you add the flag "--upgrade" to the install command:
```cli
pip install --upgrade {package-name}
```

## Removing Packages
To remove a package, you use the uninstall command:
```cli
pip uninstall {package-name}
```

## Viewing Packages Installed
There are two options for viewing your currently installed packages: list and freeze. List creates a human-friendly printout of your installed packages and their versions:
```cli
pip list
Package      Version
------------ -------
package-one  1.0.0
package-two  1.1.0
...
```
The freeze command outputs the packages in a format that pip could use to interact with the packages at a later date:
```cli
pip freeze
package-one==1.0.0
package-two==1.1.0
...
```
The output of the freeze command is often redirected to a file called "requirements.txt" to track which packages and their versions are required for the application. This also makes it easy to perform batch operations on your packages.

## Batch Operations
If you need to install all the packages in the requirements.txt file, you can use the "-r" flag and the path to the requirements file to tell pip to install the packages found in the file:
```cli
pip install -r requirements.txt
```
You can do the same to uninstall packages:
```cli
pip uninstall -r requirements.txt
```

</details>
<details><summary>Summary</summary>

# Summary

- Pip is a package management software.
- PyPI is the main repository for packages, and pip downloads from it.
- Common practice is to save package information in a file called "requirements.txt."

