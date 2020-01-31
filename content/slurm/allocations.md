---
title: "Allocations"
date: 2020-01-06T17:22:32Z
weight: 2
---

## Determining what resources to request

Before submitting a job for processing, it is essential to know the requirements of your application so that it can be run properly. Because each application has unique requirements it is advisable to determine what resources you need before you submit your script.

Do not forget that while increasing the amount of compute resources you request may decrease the time it takes to run your job, it will also increase the time you have to wait in queue for using those resources. If you think that your job will not finish in under 2 hours, use the long-run queue instead of the base queue. 

## Queues 

There are several queues present in the machines and different users may access different queues. All queues have different limits in amount of cores for the jobs and duration. You can check anytime all queues you have access to and their limits using:

The standard configuration and limits of the queues are the following


| Queue | Maximum number of nodes (cores)| Maximum wallclock |
|---|---|---|
|base	 | infinite |	2 h |
|longrun |	infinite |	6 h |


For longer and/or larger executions special queues are available upon request and will require proof of scalability and application performance. To solicit access to these special queues please contact us.


