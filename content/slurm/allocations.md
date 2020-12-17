---
title: "Allocations"
date: 2020-01-06T17:22:32Z
weight: 3
---

## Determining what resources to request

Before submitting a job for processing, it is essential to know the requirements of your application so that it can be run properly. Because each application has unique requirements it is advisable to determine what resources you need before you submit your script.

Do not forget that while increasing the amount of compute resources you request may decrease the time it takes to run your job, it will also increase the time you have to wait in queue for using those resources. 

Be sure to request computing resources e.g., number of nodes, number of tasks per node, max time per job, that are consistent with the type of application(s) you are running:

* A **serial (non-parallel) application** can only make use of a single core on a single node, and will only see that node's memory.

* A **threaded program (e.g. one that uses OpenMP)** employs a **shared memory programming** model and is also restricted to a single node, but the program's individual threads can run on multiple cores on that node.

* An **MPI (Message Passing Interface)** program can **exploit the distributed computing power of multiple nodes:** it launches multiple copies of its executable (MPI tasks, each assigned unique IDs called ranks) that can communicate with each other across the network. The tasks on a given node, however, can only directly access the memory on that node. Depending on the program's memory requirements, it may not be possible to run a task on every core of every node assigned to your job. If it appears that your MPI job is running out of memory, try launching it with fewer tasks per node to increase the amount of memory available to individual tasks.


## Queues 

There are several queues present in the machines and different users may access different queues. All queues have different limits in amount of cores for the jobs and duration. You can check anytime all queues you have access to and their limits using:

The standard configuration and limits of the queues are the following


| Queue | Maximum Nodes Per Job | Maximum Nodes Per User | Maximum Job Time |
|---|---|---|---|
|base	 | 48 | 144	| 24 h |


For longer and/or larger executions special queues are available upon request and will require proof of scalability and application performance. To solicit access to these special queues please contact us.
