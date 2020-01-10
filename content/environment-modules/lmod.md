---
title: "Lmod"
date: 2020-01-06T17:22:32Z
---

Lmod is a module system that offers a way to dynamically change the users environment through modulefiles, including adding and removing directories from the PATH environment variable. In order to the user communicate with Lmod, it has a list of commands to interact with it.

## Module Commands

The _module_ command sets the proper environment variable, independently of the user's shell. Typically, a system will load a default set of modules.

### Listing loaded modules

In order to find which modules are loaded, a user can do:

```bash
$ module list
```

### Available modules

To find out which modules are available to be loaded, a user can do:

```bash
$ module available

-------------------------- /opt/ohpc/pub/macc/modules/sandybridge/modules/all ---------------------------
   Autoconf/2.69-GCCcore-6.4.0                    Ninja/1.9.0-GCCcore-8.2.0                       
   Autoconf/2.69-GCCcore-8.2.0             (D)    OpenBLAS/0.2.20-GCC-6.4.0-2.28                  
   Automake/1.15.1-GCCcore-6.4.0                  OpenBLAS/0.3.5-GCC-8.2.0-2.31.1             (D) 
   Automake/1.16.1-GCCcore-8.2.0           (D)    OpenFOAM/v1812-foss-2019a                       
   Autotools/20170619-GCCcore-6.4.0               OpenFOAM/v1906-foss-2019a                      
   Autotools/20180311-GCCcore-8.2.0        (D)    OpenFOAM/6-foss-2019a                       (D) 
   Bison/3.0.4-GCCcore-6.4.0                      OpenMPI/2.1.1-GCC-6.4.0-2.28                   
   Bison/3.0.4                                    OpenMPI/3.1.3-GCC-8.2.0-2.31.1              (D)
   Bison/3.0.5-GCCcore-6.4.0                      PCRE/8.43-GCCcore-8.2.0                        
   Bison/3.0.5-GCCcore-8.2.0                      PETSc/3.11.1-foss-2019a                        
   Bison/3.0.5                                    ParMETIS/4.0.3-foss-2017b                      
   Bison/3.3.2                             (D)    ParMETIS/4.0.3-gompi-2019a                  (D)
   Boost/1.70.0-gompi-2019a                       ParMGridGen/1.0-foss-2017b                     
   CFITSIO/3.47-GCCcore-8.2.0                     ParMGridGen/1.0-foss-2019a                  (D)
   CGAL/4.11.1-foss-2019a-Python-3.7.2            Perl/5.28.1-GCCcore-8.2.0                      
   CGAL/4.14-foss-2019a-Python-3.7.2       (D)    Python/2.7.14-foss-2017b                       
   CMake/3.9.1-GCCcore-6.4.0                      Python/2.7.15-GCCcore-8.2.0                    
   CMake/3.9.5-GCCcore-6.4.0                      Python/2.7.16-GCCcore-8.2.0                    
   CMake/3.13.3-GCCcore-8.2.0              (D)    Python/3.7.2-GCCcore-8.2.0                  (D)
   Eigen/3.3.7                                    ROOT/6.18-GCCcore-8.2.0                        
   FFTW/3.3.6-gompi-2017b                         SCOTCH/6.0.4-foss-2017b                        
   FFTW/3.3.8-gompi-2019a                  (D)    SCOTCH/6.0.6-gompi-2019a                    (D)
   GCC/6.4.0-2.28                                 SQLite/3.20.1-GCCcore-6.4.0                    
   GCC/8.2.0-2.31.1                        (D)    SQLite/3.27.2-GCCcore-8.2.0                 (D)
```

These are a few packages available on MACC.

### Loading and unloading modules

To load packages a user can do:

```bash
$ module load packageA packageB
```

In the same manner, a user can unload packages with:
```bash
$ module unload packageA packageB
```

It may happen that a user wants to change, for example, his OpenFOAM version. So if the user that already has the version _v1812-foss-2019a_ and needs the _v1906-foss-2019a_ version, he can just do:

```bash
$ module swap OpenFOAM/v1812-foss-2019a OpenFOAM/v1906-foss-2019a 
```

### Resetting and restoring modules

If a user wants to unload all currently loaded modules he has 2 options, either he can go back to a default set of modules, with:

```bash
$ module reset
```

This will unload all the modules and then load the list specified by LMOD_SYSTEM_DEFAULT_MODULES variable.

The other option is restoring the modules to the user default, with

```bash
$ module restore
```

### Module information

In case the user needs a description of what the modules does, he can do:

```bash
$ module whatis moduleA
```

## Useful commands

Writing _module_ every time a user wants to execute a command is boring, so Lmod provides the **ml** tool. The most common command are _module list_ and _module load<\_>_, the **ml** command does both:

```bash
$ ml
```
This is equivalent to _module list_, and:
```bash
$ ml moduleA
```
means _module load moduleA_ while:

```bash
$ ml -moduleA
```

means _module unload moduleA_. You can also combine them:

```bash
$ ml -moduleA moduleB
```

meaning _module unload moduleA; module load moduleB_.

You can also do other module commands:

```bash
$ ml avail
$ ml whatis moduleA
$ ml show moduleB
```

So, instead of using _module_ you can use _ml_.
