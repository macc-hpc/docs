---
title: "MACC Citizenship"
date: 2020-12-15T18:38:09Z
weight: 2
pre: "<b>2. </b>"
---
You share Bob with many users, and what you do on the system affects others. Thus, users must follow a code of conduct in which the users limit activities that may impact the system for other users. 

## MACC Law Abiding Citizen

#### MACC golden rules:

* **Do Not Run Jobs on the Login Nodes**
* **Do Not Stress the File Systems**
* **Limit Input/Output (I/O) Activity**
* **Limit File Transfers**

### Do Not Run Jobs on the Login Nodes

Bob's login nodes are shared among all users. Dozens of users may be logged on at one time accessing the file systems. Think of the login nodes as a prep area, where users may 
* edit and manage files
* compile code
* perform file management
* issue transfers
* submit new and track existing batch jobs
* etc. 

The login nodes provide an interface to the "back-end" compute nodes.

The compute nodes are where actual computations should occur and where research is done. Hundreds of jobs may be running on all compute nodes, with hundreds more queued up to run. **All batch jobs and executables, as well as development and debugging sessions, must be run on the compute nodes.** To access compute nodes on MACC resources, one must either submit a job to a batch queue or initiate an interactive session.

A single user running computationally expensive or disk intensive task/s will negatively impact performance for all other users. Thus, **Do not run jobs or perform an intensive computational activity on the login nodes or the shared file systems.Your account may be suspended.**

<!-- Running jobs on the login nodes is one of the fastest routes to account suspension. Instead, run on the compute nodes via an interactive session (idev or by submitting a batch job.

We stress this aggain, **Do not run jobs or perform an intensive computational activity on the login nodes or the shared file systems.
Your account may be suspended.** and you will lose access to the queues if your jobs are impacting other users.**-->

#### Do's & Don't on the Login Nodes
<!-- 
Do not run research applications on the login nodes; this includes frameworks like MATLAB and R, as well as computationally or I/O intensive Python scripts. If you need interactive access, use the idev utility or Slurm's srun to schedule one or more compute nodes.

**DO THIS**: Start an interactive session on a compute node and run Matlab.

```bash
  $ project=acctxxx #Project to which the value of the interactive session will be discounted
  $ idev $project 
    nid00181$ matlab
```

**DO NOT DO THIS**: Run Matlab or other software packages on a login node
```bash
$ matlab
```

Do not launch too many simultaneous processes; while it's fine to compile on a login node, a command like "make -j 16" (which compiles on 16 cores) may impact other users.
 -->

**DO THIS**: build and submit a batch job. All batch jobs run on the compute nodes.

```bash
 $ make mytarget
 $ sbatch myjobscript
```

**DO NOT DO THIS**: invoke multiple build sessions, run an executable on a login node.

```bash
$ make -j 16
$ ./myprogram
```
<!-- That script you wrote to poll job status should probably do so once every few minutes rather than several times a second. -->

### Do Not Stress the Shared File Systems

We recommend that you run your jobs out of your resource's **$SCRATCH** file system instead of **$HOME** file system. 

To run your jobs out **$SCRATCH**:

* Copy or move all job input files to **$SCRATCH**
* Make sure your job script directs all output to **$SCRATCH**

Consider that **$HOME** is for storage and keeping track of important items. Actual job activity, reading and writing to disk, should be offloaded to your resource's **$SCRATCH** file system.

You can start a job from anywhere but the actual work of the job should occur only on the **$SCRATCH** partition.
 
You can save original items to **$HOME** so that you can copy them over to **$SCRATCH** if you need to re-generate results.

### Limit Input/Output (I/O) Activity

<!-- In addition to the file system tips above, it's important that your jobs limit all I/O activity. This section focuses on ways to avoid causing problems on each resources' shared file systems. -->

**Avoid I/O intensive sessions** (lots of reads and writes to disk, rapidly opening or closing many files)

Every open/close operation on the file system requires interaction with the MetaData Service (MDS). The MDS acts as a gatekeeper for access to files on Lustre's parallel file system. Overloading the MDS will affect other users on the system. If possible, open files once at the beginning of your program/workflow, then close them at the end.

We also recommend the usage of the **hdf5** or **NetCDF** libraries to generate a single restart file in parallel, rather than generating files from each process separately.

<!-- Avoid opening and closing files repeatedly in tight loops. Every open/close operation on the file system requires interaction with the MetaData Service (MDS). The MDS acts as a gatekeeper for access to files on Lustre's parallel file system. Overloading the MDS will affect other users on the system. If possible, open files once at the beginning of your program/workflow, then close them at the end.

Don't get greedy. If you know or suspect your workflow is I/O intensive, don't submit a pile of simultaneous jobs. Writing restart/snapshot files can stress the file system; avoid doing so too frequently. Also, use the hdf5 or netcdf libraries to generate a single restart file in parallel, rather than generating files from each process separately.

If you know your jobs will require significant I/O, please submit a support ticket and an HPC consultant will work with you. See also Managing I/O on MACC Resources for additional information. -->

### Limit File Transfers

In order to not stress both internal and external networks:

* **Avoid too many simultaneous file transfers**. You share the network bandwidth with other users; don't use more than your fair share. Two or three concurrent scp sessions is probably fine. Twenty is probably not.

* **Avoid recursive file transfers**, especially those involving many small files. **Zip files before transferring them**.

* **When creating or transferring large files stripe the receiving directories**.
 <!-- See STRIPING for more information. -->