# Using Slurm

In order to understand how Slurm is used in practice, we will present a practical case and then explain how we can use Slurm for its execution, as well as managing its life cycle.

Now that everything is ready, the next step is to use Slurm to execute your job.

## Before starting

Before submitting a job is important to have a general overview of the cluster. For instance, it is important to know the resources offered by the cluster and which jobs are currently allocating them.

For this purpose, the _sinfo_ command can be used to get a overview of the resources offered by the cluster, while the _squeue_ command shows which jobs are the resources allocated to.

```bash
$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
base*        up 2-00:00:00      2 drain* c806
base*        up 2-00:00:00    154  down* c805
longrun      up 6-00:00:00     33  alloc c823
longrun      up 6-00:00:00      5   idle c824
```

The above command shows the output of a _sinfo_ execution, showing some info about the cluster. In the first column, we see the available queues on the cluster, being in this case, _base_ and _longrun_. Usually each of this partitions are used for different purposes. As we can see in the example, the base partition (default) is used for faster jobs, allowing at most 48 hours of execution time. In case the users need to run jobs for longer than that, they can use the _longrun_ partition which support jobs running at most for 144 hours (6 days).

It is also useful so check the queues to see which jobs are already running, their size and how much time you will have to wait until your job starts executing. 

```bash
$ squeue
JOBID PARTITION     NAME   USER  ST       TIME   NODES NODELIST(REASON)
6969   longrun 		jobW   userA  R     23:59:05   16 	c823
6970   longrun 		jobX   userB  R      5:02:27   16 	c825
7004   base   		jobY   userC  R   1-23:00:01   1 	c806
7005   base    		jobZ   userD  PD      0:00     32 	c812
```
 
Here, we can see which jobs are running, with the state *R*, short for running, and which are waiting for resources *PD*, short for pending.


## Creating a job

The first thing to know before creating a job is that it is composed by two parts: jobs steps and resources. Job steps are tasks by which the main job is composed, while resources consist in amounts of CPU, RAM, disk space and computing time.

The most common way to create a job is to write a shell script. For example, in the script below is a simple job where one CPU is requested for one minute along with 100MB of RAM for the job execution. The directives _*SBATCH*_ must appear before the actual script begins, between the shebang and the actual script.

```bash
#!/bin/bash
#
#SBATCH --job-name=Test
#SBATCH --output=hello.txt
#
#SBATCH --ntasks=1
#SBATCH --time=01:00
#SBATCH --mem-per-cpu=100

srun echo "Hello Bob!"
```

In order to submit a shell script for execution we can use the _sbatch_ command, 