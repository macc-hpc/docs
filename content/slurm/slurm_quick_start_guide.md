---
title: "Slurm Quick Start Guide"
date: 2020-01-06T17:22:32Z
weight: 1
---

## Architecture

As shown in Figure 2, Slurm is composed by management daemons and, the **slurmctld** that runs on the management node and **slurmd** that runs on every compute node. The figure X presents the architecture of a Slurm cluster.

{{< figure src="https://slurm.schedmd.com/arch.gif" title="Slurm architecture" link="https://slurm.schedmd.com/quickstart.html" >}} 


In order to interact with the cluster the user as a list of commands that can be used to multiple purposes. This lists include the following commands: **sacct**, **salloc**, **sattach**, **sbatch**, **sbcast**, **scancel**, **sinfo**, **smap**, **squeue**, **srun**, **strigger** and **sview**. These commands can be executed in any node of the cluster.

## User Commands

A brief description of the Slurm commands referred above.

**sacct**
 - Used to report a job or accounting information about active or completed jobs.

**salloc**
 - Used to allocate resources for a job and spawn a shell, is then used to execute **srun** commands to launch tasks.

**sattach**
 - Used to attach standard input, output and error to a currently running job or step.

**sbatch**
 - Used to submit a job script for later execution. This script is, typically composed of one or more **srun** commands to launch parallel tasks.

**sbcast**
 - Used to transfer a file from a local disk to local disk on the nodes allocated to a job.

**scancel**
 - Used to cancel a pending or running job or job step. Also, it can be used to send arbitrary signals to all processes associated with the running job or job step.

**sinfo**
 - Reports the state of partitions and nodes managed by Slurm, supporting filtering, sorting and formatting options.

**smap**
- As the same purpose as **sinfo** but displays the information graphically.

**squeue**
 - Reports the state of jobs or job steps. by default, it reports the running jobs in priority order and then the pending jobs in priority order.

**srun**
 - Used to submit a job for execution or start job steps in real time. This command has a wide set of options to specify resource requirements and specific node characteristics. A job can be composed by multiple job steps executing sequentially or in parallel on independent or shared resources within the job's node allocation.

**strigger**
 - Used to create, get and view event triggers, such as nodes going down or jobs reaching their time quota.

**sview**
 - A graphic user interface to get and update state information for jobs, partitions and nodes in the Slurm cluster.