# SBILL-SLURM
Query SLURM billing per job via SLURM sacct command

SBILL version:
1.4.6 (24 August 2024)

Dependencies:
+ python (>=3.1.0)  -- subprocess, math, os, sys, str.format
+ numpy  (>=1.11.0) -- Optional, only for --histogram option
+ SLURM

Note:
1. When doing timely utilization reports, the --truncate option (from sacct) must be used for correctness.
2. AllocMem field does not follow the unit specified by --units. 
