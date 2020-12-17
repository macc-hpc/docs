---
title: "Billing"
date: 2020-12-17T17:38:51Z
wheight: 2
---

The Slurm scheduler tracks and charges for usage to a granularity of a few seconds of wall clock time. 

**The system charges only for the resources you actually use, not those you request**.

 If your job finishes early and exits properly, Slurm will release the nodes back into the pool of available nodes. Your job will only be charged for as long as you are using the nodes.

**MACC does not implement node-sharing on any compute resource**. Thus, a node can only be assigned to one user at a time; hence a complete node is dedicated to a user's job and accumulates wall-clock time for all the node's cores whether or not all cores are used.

### Examples

The most common way to create a job is to write a shell script.
For example, in the scripts below we will show simple examples to re
is a simple job where one CPU is requested for one minute along with 100MB of RAM for the job execution. The directives **SBATCH** must appear before the script begins, between the shebang and the script.

```bash
#!/bin/bash
...                         # previous SBATCH configuration
#SBATCH --nodes=1           # allocation of 1 node
#SBATCH --ntasks=1          # allocation of 1 CPU
#SBATCH --time=01:00        # allocation for 1 minute
srun echo "Hello Bob!"
```

```bash
#!/bin/bash
...                         # previous SBATCH configuration
#SBATCH --nodes=1           # allocation of 1 node
#SBATCH --ntasks=16         # allocation of 16 CPUs
#SBATCH --time=01:00        # allocation for 1 minute
srun echo "Hello Bob!"
```

```bash
#!/bin/bash
...                         # previous SBATCH configuration
#SBATCH --nodes=1           # allocation of 1 node
#SBATCH --ntasks=4          # allocation of 4 CPU
#SBATCH --time=01:00        # allocation for 1 minute
srun echo "Hello Bob!"
```

```bash
#!/bin/bash
...                         # previous SBATCH configuration
#SBATCH --nodes=4           # allocation of 1 node
#SBATCH --ntasks=64         # allocation of 64 CPU (4 Nodes *16)
#SBATCH --time=01:00        # allocation for 1 minute
srun echo "Hello Bob!"
```

This will translate into the following billing table.

|#Nodes|#Cores|Bill|
|---|---|---|
|1|1|16 Min|
|1|16|16 Min|
|4|1|64 Min|
|4|16|64 Min|

The resources are **not shared**. When allocating a node, the full 16 CPUs (cores) from that node will be allocated whether or not all cores are used.

Users with an account at MACC may consult their current bills 

```bash
$ billing
# or 
$ maccinfo
```