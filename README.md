# SBILL-SLURM
Query SLURM job billing and information -- a Python wrapper of SLURM SACCT command

SBILL version:
1.5.2 (21 May 2025)

Dependencies:
+ python (>=3.3.0)  -- subprocess, math, os, sys, str.format, datetime
+ numpy  (>=1.11.0) -- Optional, only for --histogram option
+ SLURM

*** ANNOUNCEMENT *** \
If you encounter any issues employing/using SBILL-SLURM on your system, you could also submit an issue on this GitHub.
We will try our best to assist you, since we have become aware that certain SLURM versions and configurations may require additional adjustments.

-----
```txt
Usage: sbill [OPTIONS(0)...]

Query job billing and information

JOB FILTER/QUERY OPTIONS:
  -j, --jobs=<jobid,...>            jobs in the specified list
      --name=<jobname,...>          jobs that have these name(s)

  -A, --accounts=<account,...>      jobs charged to these account(s)
                                      Default: all of yours
  -a, --allusers                    jobs submitted by any users
  -u, --user=<username,...>         jobs submitted by these user(s)
                                      Default: only you
  -g, --group=<group,...>           jobs started with the group(s)

  -L, --allclusters                 jobs on any clusters
      --local                       jobs on local cluster
  -M, --clusters=<cluster,...>      jobs started on the cluster(s)
      --associations=<assoc,...>    jobs under the association(s)
      --federation                  jobs from the federation

  -p, --partition=<partition,...>   jobs on these partition(s)
  -w, --nodelist=<nodename,...>     jobs on these node(s)
      --reservation=<reserv,...>    jobs that run using these reservation(s)
      --state=<job_state,...>       jobs that are marked with these state(s)

      --constraints=<contraint,...> jobs requesting these constraint(s)
  -q, --qos=<qos,...>               jobs that run using these QoS
  -W, --wckeys=<wckey,...>          jobs with specified wckey(s)

  -N, --nnodes=<num> or <min-max>   jobs that get the specified number of nodes
  -C, --ncpus=<num> or <min-max>    jobs that get the specified number of CPUs
  -G, --ngpus=<num> or <min-max>    jobs that get the specified number of GPUs
      --ram=<min[-max]>             jobs that get RAM  within the specified range

      --range=<min[-max]>           jobs charged within the specified 'Service' range
      --runtime=<min[-max[:unit]]>  jobs that have runtime within the range
      --waittime=<min[-max[:unit]]> jobs that have waittime within the range
                                    where unit of them is 'sec', 'min', or 'hr'
                                      Default: in 'hr' unit 

  -E, --endtime=<time>              jobs that start before this time point
                                      Default: now
  -S, --starttime=<time>            jobs that end after this time point
                                      Default: today at 00:00:00
                                    where the format of <time> is...          
                                      YYYY-MM-DD[THH:MM[:SS]] or              
                                      MM/DD[/YY]-HH:MM[:SS] or                
                                      MMDD[YY] or MM/DD[/YY] or MM.DD[.YY] or 
                                      now[{+|-}count[second|minute|hour|day|week]]
  Warning: When using -S and -E to get a net utilization within a time window,
           -T, --trim or --truncate MUST be used for correctness.

  -T, --trim, --truncate (slurm)    trim job runtime by trunicating start/end time
                                    according to -S, -E options
      --helptrim, --helptruncate    detailed explanation regarding -T, --trim

JOB DISPLAY/OUTPUT OPTIONS:
  -l, --long                        display the jobs in SBILL long format
  -o, --format=<field,...>          list of fields to be displayed where... 
                                     = Column width/precision can be set by
                                       <field>%<width>
                                     = User's default format can be set by
                                       export SBILL_FORMAT=<field,...>
      --helpformat                  display all available fields, then exit

  -H, --histogram=<nbin>[:field]    display text-based histogram of the jobs.
                                    use --histogram=help to see available fields
                                      Default: Service
  --timeseries=[field:]<step-hour>  display time-series table of utilization
                                    and a text-based graph of the specified field
                                      Default: Service

  -X, --summary                     display only the summary report
      --sum-by-account              display sum(s) of the filtered jobs by account
      --sum-by-user                 display sum(s) of the filtered jobs by user
      --sumby[xxx]                  various aliases of --sum-by-xxx
                                    where xxx must be either account or user

      --to_csv=<filename>           save job records in CSV format to <filename>
      --csv_sep=<character>         separator/delimiter for --to_csv option

OTHERS:
  -h, --help                        print this help message, then exit
  -V, --version                     print SBILL version and few details, then exit
      --units=[KMGTP]               specify RAM memory unit. Default: G (GiB)
      --scientific                  use scientific number format (e)
```

| Example: sbill --long xxx|
| :-----------------: |
| ![](Example_long.png) |

| Example: sbill --sumbyuser xxx|
| :-----------------: |
| ![](Example_sumby.png) |

| Example: sbill --histogram xxx|
| :-----------------: |
| ![](Example_histogram.png) |

| Example: sbill --timeseries xxx|
| :-----------------: |
| ![](Example_timeseries.png) |

