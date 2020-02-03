---
title: "Using Python"
date: 2020-01-06T17:22:32Z
weight: 3
---

Python is a interpreted high level language that emphasizes code readibility and productivity. This, as other reasons, has driven its growth in sciences and make it a must in HPC clusters. Macc comes with a variety of Python distributions:
 - Python 2.7.14
 - Python 2.7.15
 - Python 2.7.16
 - Python 3.7.2  

These installations may come with packages often needed in HPC environments, however, there are Python packages which do not fit in the Python installation tree. Sometimes, the users need to have the flexibilty to install packages without having to install their own Python distribution.

**Python Virutal Environment** solves this problems by allowing the users to create a virtual distribution from an existing Python installation. We can see a more detailed view of the Python installed distributions by:

```bash
$ ml av Python
-------------- /opt/ohpc/pub/macc/modules/sandybridge/modules/all --------------
   Python/2.7.14-foss-2017b       Python/2.7.16-GCCcore-8.2.0
   Python/2.7.15-GCCcore-8.2.0    Python/3.7.2-GCCcore-8.2.0  (D)

  Where:
   D:  Default Module

```

As there are some differences between creating a Virtual Environment under Python 2.x and Python 3.x, there will be 2 sections explaining the setup on both versions.

## Virtual Environment (Python 2.x)

Before we setup the virtual environment, we must have virtualenv installed in the main distribution.

### Creating a Virtual Environment

By default, MACC uses a Python 3.x distribution, as we can see with `ml av Python` command. In this section we will use Python 2.7.16 as an example.

```bash
$ ml Python/2.7.16-GCCcore-8.2.0 # Loads Python distribution
$ virtualenv --system-site-packages VirtualEnvNAME-Python-2.7.16 # Creates the virtual environment
$ ml -Python/2.7.16-GCCcore-8.2.0 # Unloads Python distribution
```
The flag *--system-site-packages* allows the use of packages installed in the main distribution.


### Activation of the Virtual Environment 

```bash
$ source VirtualEnvNAME-Python-2.7.16 # Activates the virtual environment
```

You can check if your virtual environment is being used by using `which python` that should result on *VirtualEnvNAME-Python-2.7.16/bin/python*.

### Packages installation on the virtual environment 

To install the packages that you need, you can simply:

```bash
$ pip install PACKAGE_NAME
```


## Virtual Environment (Python 3.x)

In the same manner as the previous section, we can see and load which python distribution we want to use, being Python 3.7.2 the focus of this section. It can be load and unloaded with the same lmod commands.

```bash
$ ml Python/3.7.2-GCCcore-8.2.0 # Loads Python distribution
$ virtualenv --system-site-packages VirtualEnvNAME-Python/3.7.2 # Creates the virtual environment
$ ml -Python/3.7.2-GCCcore-8.2.0 # Unloads Python distribution
```
The flag *--system-site-packages* allows the use of packages installed in the main distribution.


### Activation of the Virtual Environment 

```bash
$ source VirtualEnvNAME-Python-3.7.2 # Activates the virtual environment
```

You can check if your virtual environment is being used by using `which python` that should result on *VirtualEnvNAME-Python-3.7.2/bin/python*.

### Packages installation on the virtual environment 

To install the packages that you need, you can:

```bash
$ python -m pip install PACKAGE_NAME
```
