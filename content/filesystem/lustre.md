---
title: "File Systems"
date: 2020-01-06T17:22:32Z
---

Each user has several areas of disk space for storing files. These areas may have size or time limits, please read carefully all this section to know about the policy of usage of each of these filesystems. There are 3 different types of storage available inside a node:

* Lustre filesystems: Lustre is a distributed networked filesystem which can be accessed from all nodes, login and compute
* Local hard drive: Every node has an internal hard drive

## Lustre Filesystem
The Lustre File System is a high-performance shared-disk file system providing fast, reliable data access from all nodes of the cluster to a global filesystem. Lustre allows parallel applications simultaneous access to a set of files (even a single file) from any node that has the Lustre file system mounted while providing a high level of control over all file system operations. In addition, Lustre can read or write large blocks of data in a single I/O operation, thereby minimizing overhead.

These are the Lustre filesystems available in the machine from all nodes:

* /home: This filesystem has the home directories of all the users, and when you log in you start in your home directory by default. Every user will have their own home directory to store own developed sources and their personal data. Also, it is highly discouraged to run jobs from this filesystem. Please run your jobs on /scratch instead.

* /fs/scratch: Each user will have a directory over /fs/scratch. Its intended use is to store temporary files of your jobs during their execution. 

## Local Hard Drive
Every node has a local solid state (SSD) hard drive (HDD) that can be used as a local scratch space to store temporary files during executions of one of your jobs. This space is mounted over /tmp/ directory. The amount of space within the /tmp filesystem is about 8 GB. All data stored in these local hard drives at the compute nodes will not be available from the login nodes.

##  Quotas

Bob mounts the two file systems that are shared across all nodes: **home** and **scratch**.

The system also defines for you corresponding account-level environment variables $HOME and $SCRATCH. Consult Table  

 for quota and purge policies on these file systems.

Several aliases are provided for users to move easily between file systems:
* Use the "cdh" or "cd" commands to change to $HOME
* Use the "cds" command to change to $SCRATCH

|  **File System**   |     **Quota**      |
| ------------------ | ------------------ |
|         HOME       |         50G        |
|       SCRATCH      |          1T        |