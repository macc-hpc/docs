---
title: "Compilers"
date: 2020-01-21T19:52:32Z
weight: 1
---

## C Compilers
In the cluster you can find these C/C++ compilers :

gcc /g++ -> GNU Compilers for C/C++

    % man gcc
    % man g++
All invocations of the C or C++ compilers follow these suffix conventions for input files:
* .C, .cc, .cpp, or .cxx -> C++ source file.
* .c -> C source file
* .i -> preprocessed C source file
* .so -> shared object file
* .o -> object file for ld command
* .s -> assembler source file

By default, the preprocessor is run on both C and C++ source files.

These are the default sizes of the standard C/C++ datatypes on the machine

Default datatype sizes on the machine 


|Type|	Length (bytes)|
|---|---|
|bool (c++ only)|	1|
|char|	1|
|wchar_t|	4|
|short|	2|
|int|	4|
|long|	8|
|float|	4|
|double|	8|
|long double|	16|

## Distributed Memory Parallelism
To compile MPI programs it is recommended to use the following handy wrappers: mpicc, mpicxx for C and C++ source code. You need to choose the Parallel environment first: *module load openmpi*. These wrappers will include all the necessary libraries to build MPI applications without having to specify all the details by hand.

    % mpicc a.c -o a.exe
    % mpicxx a.C -o a.exe 