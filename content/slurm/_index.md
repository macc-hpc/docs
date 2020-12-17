---
title: "Running Jobs"
date: 2020-01-06T17:22:32Z
weight: 6
pre: "<b>6. </b>"
---

<!-- Slurm is the utility used for batch processing support, so all jobs must be run through it. This section provides information for getting started with job execution at the Bob cluster. -->


Bob's job scheduler is the **Slurm** Workload Manager. Slurm commands enable you to submit, manage, monitor, and control your jobs. Jobs submitted to the scheduler are queued, then run on the compute nodes.

<!-- **Each job consumes core-hours which are then charged to your project**. -->
**MACC's accounting system is based on core-hours per Project.**


The system charges only for the resources you actually use, not those you request. In Bobs' instance resources are not shared , this is, when allocating a node, the full 16 CPUs (cores) from that node will be used. This has an impact on the billing system.
If your job finishes early and exits properly, Slurm will release the nodes back into the pool of available nodes and finishes charging. Your job will only be charged for as long as you are using the nodes.


> **Billing = (#nodes) x (#cores = 16) x (job duration)**

MACC does not implement node-sharing on any compute resource. In Bobs' case the **billing will allways collect the value of the 16 CPUs**.

Users with an account at MACC may consult their current bills 

```bash
$ billing
# or 
$ maccinfo
```