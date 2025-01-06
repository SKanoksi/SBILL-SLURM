# SBILL-SLURM
Query SLURM billing per job through SLURM sacct command

SBILL version:
1.5.0 (06 January 2025)

Dependencies:
+ python (>=3.1.0)  -- subprocess, math, os, sys, str.format
+ numpy  (>=1.11.0) -- Optional, only for --histogram option
+ SLURM

Note:
1. When doing timely net utilization reports, the -T, --trim, --trim-job or --truncate option (from sacct) must be used for correctness.
2. AllocMem field does not follow the unit specified by --units. 

| Example:|
| :-----------------: |
| ![](Example.png) |


-----
```txt
Usage: sbill [OPTIONS]

Query job billing and information

OPTIONS:
  -A, --accounts=<slurm_account_list>
      specify one or more accounts

  -a, --allusers
      display jobs of all users

  -L, --allclusters
      display jobs ran on all clusters

  -E, --endtime=<slurm_end_time>
      display only jobs that start running before this end time (Also see --truncate)

  -o, --format=<slurm/sbill_field_list>
      specify fields to be displayed, e.g., 'JobID,JobName,State%9,Service' (see --helpformat)
      Note:
      - Column width can be fixed by using '<field>%<width>'. The default is unlimited.
      - Set 'SBILL_FORMAT' environment variable to override the default format.
      - Please note that CPU-core-hour and GPU-card-hour are of allocation.

  -h, --help
      show this help message and exit

  --helpformat
      print the fields that can be specified with the --format option

  -H, --histogram=<number_of_bins>[:field]
      quickly compute histogram of the displayed jobs using the input number of bins
      [Note: The supported fields are Service, CPU-core-hour, GPU-card-hour,
                                      NNode, NCPU, NGPU, RunSec, RunMin, RunHour]

  -j, --jobs=<slurm_job>
      display only the specified job

  -l, --long
      equivalent to '--format=JobID,JobName%10,User,Account,Partition,NNodes,NCPUS,NGPUS,AllocRam,NodeList%24,Elapsed,State,Service'

  --name=<slurm_jobname_list>
      display only jobs that have these names

  -i, --nnodes=<num> or <min-max>
      display only jobs that ran with the specified number of nodes

  --ncpus=<num> or <min-max>
      display only jobs that ran with the specified number of CPUs

  --ngpus=<num> or <min-max>
      display only jobs that ran with the specified number of GPUs

  --noconvert
      do not convert units, e.g., 2048M won't get converted to 2G

  -N, --nodelist=<slurm_node_list>
      display only jobs that ran on these nodes

  -r, --partition=<slurm_partition_list>
      display only jobs that ran on these partitions

  --range=<min[-max]>
      specify min and max of Service to filter jobs

  --to_csv=<filename>
      save as .csv file

  -S, --starttime=<slurm_start_time>
      display only jobs that stop running after this start time (Also see --truncate)
      Note: On this system, the billing start at 2025-01-06T00:00:00

  --state=<COMPLETED,FAILED,CANCELED,TIMEOUT,...>
      display only jobs marked with these state (no abbreviation)

  --sum-by=[Account,User], --sumby=[Account,User]
      sum Service of the displayed jobs by [Account or User]
  --sum-by-account, --sumbyaccount, --sum-byaccount, --sumby-account
      equivalent to --sumby=Account
  --sum-by-user, --sumbyuser, --sum-byuser, --sumby-user
      equivalent to --sumby=User

  -T, --trim, --trim-jobtime, --truncate
      Trim job runtime or truncate start and end time of jobs, according to --starttime and --endtime
      Note: When doing a timely utilization report, this option MUST be used for correctness.

  -u, --user=<slurm_user_list>
      display only jobs submitted by these users

  --units=[KMGTP]
      display values in the specified unit type (Override --noconvert)

  -V, --version
      print version and exit

  -X, --summary
      display only the summary report (implicitly infer --trim-jobtime)

  ---------

  --> configured for XXX HPC of XXX center

```
