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
# MANDATORY - Project/Allocation name - project to whitch the job will be billed
#SBATCH --account project
# clean all loaded modules
ml purge
# load module
ml foss/2019a
 # Assign the number of processors
NPROCS=$SLURM_NTASKS
#Run the job
mpirun -n $NPROCS ./test
```

If you do not enter an account with extra time to charge the job it will not run.