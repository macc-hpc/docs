---
title: "Samples"
date: 2020-12-17T18:28:07Z
weight: 3
---


This is not a one job fits all script. Make changes regarding your particular problem.

```bash
#!/bin/bash
# Name of the job
#SBATCH --job-name=job_example
# Name of the file where job output is written, the %j will be replaced by the job id number.
#SBATCH --output=job_example-%j.log
# Number of nodes that will be allocated
#SBATCH --nodes=3
# Total number of tasks/processes that will run 24 - 8 per node (Max per node:16 - number of cores)
#SBATCH --ntasks=24
# Max job duration (hour:minute:second)
#SBATCH --time=01:00:00
# Required - Project/Allocation name - project to whitch the job will be billed
#SBATCH --account project
# clean all loaded modules
ml purge
# load module
ml foss/2019a
# Run the job
srun ./test 
```

If you do not enter an account with extra time to charge the job it will not run.

#### Common sbatch Options
|Option|Argument|Comments|
|---|---|---|
|-p|queue_name|Submits to queue (partition) designated by queue_name|
|-J|job_name|Job Name|
|-N|total_nodes| Required. Define the resources you need by specifying either: (1) "-N" and "-n"; or (2) "-N" and "--ntasks-per-node".|
|-n|total_tasks|This is total MPI tasks in this job. See "-N" above for a good way to use this option. When using this option in a non-MPI job, it is usually best to set it to the same value as "-N".|
|--ntasks-per-node or --tasks-per-node|tasks_per_node|This is MPI tasks per node. See "-N" above for a good way to use this option. When using this option in a non-MPI job, it is usually best to set --ntasks-per-node to 1.|
|-t|hh:mm:ss|Required. Wall clock time for job.|
|--mail-user=|email_address|Specify the email address to use for notifications.|
|--mail-type=|begin, end, fail, or all|Specify when user notifications are to be sent (one option per line).|
|-o or --output|output_file|Direct job standard output to output_file (without -e option error goes to this file)|
|-e or --error|error_file|Direct job error output to error_file|
|--dependency=|jobid|Specifies a dependency: this run will start only after the specified job (jobid) successfully finishes|
|-A or --account|project|Charge job to the specified project/allocation|
|-a or --array|N/A|Not available. Use the launcher module for parameter sweeps and other collections of related serial jobs.|
|--mem|N/A|Not available. If you attempt to use this option, the scheduler will not accept your job.|
|--export=|N/A|Avoid this option on Frontera. Using it is rarely necessary and can interfere with the way the system propagates your environment.|