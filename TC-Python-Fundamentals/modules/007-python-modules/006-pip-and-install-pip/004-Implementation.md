# Implementation 

## Acquiring Pip
If you downloaded Python from the main Python website or from any other major Python distributor then you should already have pip. An easy way to check is to run either of the following commands
```cli
pip --version
```
```cli
py -m pip --version
```
if the output is your version of pip then you are good to go. If you don't have it for some reason you have a few options. First try  running the "ensurepip" module
```cli
py -m ensurepip --default-pip
```
In most cases this should be enough, but if that also fails you can download a module called "get-pip.py" from [this](https://packaging.python.org/en/latest/tutorials/installing-packages/) packaging tutorial. 

If all these options fail then uninstalling and reinstalling Python from its main website will probably be your best fix.

## Installing Packages
When installing packages you have a few options for how you perform the download. The simplest way is to just use the install command
```cli
pip install {package-name}
```
Pip will try and install the most up to date version of the package. If you know you need a specific version of the package you can specify the version
```cli
pip install {package-name}=={version.number}
```
You can also specify a lower and upper bound for the version, and Pip will attempt to grab the most up to date version of your specified package that meets the requirements. There are two approaches to this option show below. The first sets a hard upper and lower bound for the version. The second option sets a "compatible" version pip checks against, and it will attempt to download the most up to date version of the package that is compatible with your chosen version. 
```cli
pip install "{package-name}>={lower.bound},<={upper.bound}"
```
```cli
pip install {package-name}~={version.you.want.compatability.with}
```
To clarify the example, image there are four version of the package:
- 0.1.1
- 0.1.2
- 0.2.1
- 0.3.1

if you specify ```pip install package~=0.1``` pip will try and download version 0.1.2, since it is not a major change from your indicated version.

## Upgrade Packages
To upgrade a package you add the flag "--upgrade" to the install command
```cli
pip install --upgrade {package-name}
```

## Removing Packages
To remove a package you use the uninstall command
```cli
pip uninstall {package-name}
```

## Viewing Packages Installed
There are two options for viewing your currently installed packages: list and freeze. List creates a human friendly print-out of your packages installed and their version. 
```cli
pip list
Package      Version
------------ -------
package-one  1.0.0
package-two  1.1.0
...
```
The freeze command outputs the packages in a format pip could use to interact with the packages at a later date
```cli
pip freeze
package-one==1.0.0
package-two--1.1.0
...
```
The output of the freeze command is often redirected to a file called "requirements.txt" to easily track what packages and their versions are required for the application. This also makes it easy to perform batch operations on your packages

## Batch Operations
If you need to install all the packages in the requirements.txt file you can use the "-r" flag and the path to the requirements file to tell pip to install the packages found in the file
```cli
pip install -r requirements.txt
```
You can do the same to uninstall packages
```cli
pip uninstall -r requirements.txt
```
