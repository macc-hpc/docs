---
title: "Billing"
date: 2020-12-17T17:38:51Z
weight: 2
---

The usage of the hours allocated to each project is of the **full responsibility of the intervenients in that project**.

To avoid bad surprises you should **only use the resources that you need**, we recommend you read the  [resources to request]({{%relref "slurm/allocations.md" %}})

The Slurm scheduler tracks and charges for usage to a granularity of a few seconds of wall clock time. 

**The system charges only for the resources you actually use, not those you request**.

 If your job finishes early and exits properly, Slurm will release the nodes back into the pool of available nodes. Your job will only be charged for as long as you are using the nodes.

**MACC does not implement node-sharing on any compute resource**. Thus, a node can only be assigned to one user at a time; hence a complete node is dedicated to a user's job and accumulates wall-clock time for all the node's cores whether or not all cores are used.


Currently, we have the policy at MACC that you **cannot order more than what you can "pay for"**. This means that if you only have X hours Free in your project you may only submit a job which bill will **not** surpass that value. Otherwise, your job would be cut down before it finished.

Thus, to fully use your project hours capability you may need to adjust the number of resources you are asking for.

> **Billing = (#nodes) x (#cores = 16) x (job duration)**



| #Hours | #Nodes | Total Billed Hours| Total Billed Minutes| Run |
|---|---|---|---|---|
|24 | 1 | 384 H | 23040 Min| |
|24 | 2 | 768 H | 46080 Min| |
|12 | 1 | 192 H | 11520 Min| X |
|12 | 2 | 384 H | 23040 Min| |
|4 | 3 | 192 H | 11520 Min| X |
|4 | 1 | 64 H | 3840 Min| X |

Imagine that you have **200 H to use** in your project.
**Only the job resource combination marked with an X would run in the queue.**


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

Users with an account at MACC may consult their your current projects and current bills 

```bash
$ billing
# or 
$ maccinfo
```