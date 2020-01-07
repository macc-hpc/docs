# Using Slurm

In order to understand how Slurm is used in practice, we will present a practical case and then explain how we can use Slurm for its execution, as well as managing its life cycle.

Let's suppose that a group of physicists want to use [OpenFOAM](https://www.openfoam.com) to study data for a CFD analysis. The first step will be moving the data to the HPC cluster where OpenFoam is installed to process this data.

Now that everything is ready, the next step is to use Slurm to execute your job.

## Before starting

Before submitting a job is important to have a general overview of the cluster. For instance, it is important to know the resources offered by the cluster and which jobs are currently allocating them.

For this purpose, the _sinfo_ command can be used to get a overview of the resources offered by the cluster, while the _squeue_ command shows which resources are allocated by submitted jobs.

```bash
$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
base*        up 2-00:00:00      2 drain* c806-[801-802]
base*        up 2-00:00:00    154  down* c805-[001-004,203,502,504,903],c806-[001-002,103,201-202,404,601,701,803],c807-[001-004,201,301-303,402,703,802,903-904],c809-[001-004,101-104,201-204,301-304,401-404,501-504,601-604,701-704,801-804,901-904],c810-[001-004,101-104,201-204,301-304,401-404,501-504,601-604,701-704,801-804,901-904],c811-[104,201,204,404,601,701,901],c812-[002,203,601,901],c813-[102,603,801,804,902],c817-[204,304,602,604],c818-[204,301,402,404,504,601],c819-[003,303,401,603-604,704,901-903],c820-[004,503,601],c821-[101,202],c822-[301,702],c823-[504,902]
base*        up 2-00:00:00      2  drain c805-303,c819-804
base*        up 2-00:00:00    206  alloc c805-[101-104,201-202,204,301-302,304,401-404,501,503,601,603-604,701-704,801-804,901-902,904],c806-[003-004,101-102,203-204,301-304,401-403,501-504,702-704,804,901-904],c811-[001-004,101-103,202-203,501-504,604,904],c812-[003-004,101-104,201-202,204,301-304,401-404,501-504,602-604,701,703-704,801,803-804,902-904],c813-901,c817-[401-404,501-504,601,603,701-704,801-804,901-903],c819-[001-002,202-204,301-302,304,501-504,601-602,701-703,801-803,904],c821-[203-204,301-304,401-403,501-504,601-602,701-704,801-804,901-904],c823-[001-004,101-104,201-204,301-304,401-404,601-604,701-704,801-803,903-904]
base*        up 2-00:00:00     95   idle c806-[104,603-604],c811-[301-304,401-403,602-603,702-704,801-804,902-903],c812-001,c813-[001-004,103-104,201-204,301-304,401-404,501-504,601-602,604,701-704,802-803,903-904],c817-[001-004,101-104,201-203,301-303,904],c819-[004,101-104,201,402-404],c821-[001-004,102-104,201,404,603-604],c823-[501-503,804,901]
base*        up 2-00:00:00    141   down c805-602,c806-602,c807-[101-104,202-204,304,401,403-404,501-504,601-604,701-702,704,801,803-804,901-902],c812-[702,802],c813-101,c818-[001-004,101-104,201-203,302-304,401,403,501-503,602-604,701-704,801-804,901-904],c820-[001-003,101-104,201-204,301-304,401-404,501-502,504,602-604,701-704,801-804,901-904],c822-[001-004,101-104,201-204,302-304,401-404,501-504,601-604,701,703-704,801-804,901-904]
longrun      up 6-00:00:00      2  down* c823-[504,902]
longrun      up 6-00:00:00     33  alloc c823-[001-004,101-104,201-204,301-304,401-404,601-604,701-704,801-803,903-904]
longrun      up 6-00:00:00      5   idle c823-[501-503,804,901]
```

