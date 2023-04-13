# SBILL-SLURM
Query SLURM billing per job via SLURM sacct command

SBILL version:
1.4.1 (06 April 2023)

Dependencies:
+ python (>=3.1.0)  -- subprocess, math, os, sys, str.format
+ numpy  (>=1.11.0) -- Optional, only for --histogram option
+ SLURM

-------------------------------------------------------

Installation:
= sbill is a single python script, internally invokes SLURM commands

1. Edit the header of sbill for your system, that is,

--------------
__HPC__ = 'XXX HPC of XXX center'             # Name of your system

key = ['billing','cpu','gres/gpu:a100']       # Keywords to be captured from alloctres field of sacct => [billing, ncpus, ngpus] fields
isRestricted = True                           # True = display only jobs related by associated accounts
SLURM_STARTDATE = '2023-04-06T00:00:00'       # Reference start date shown in --help

Service = 'Service'                                                        # Billing unit of your system                  
calService = lambda billing, elapsedraw : billing*elapsedraw/60/60/100     # How to calculate the billing
ServiceDecimal = 3                                                         # Number of decimal to be displayed.

CPUusage = 'CPU-core-hour'                                                 # CPU-usage unit to be shown
calCPUusage = lambda ncpu, elapsedraw : ncpu*elapsedraw/60/60              # How to calculate the CPU usage 
CPUusageDecimal = 2                                                        # Number of decimal to be displayed.

GPUusage = 'GPU-card-hour'                                                 # GPU-usage unit to be shown
calGPUusage = lambda ngpu, elapsedraw : ngpu*elapsedraw/60/60              # How to calculated the GPU usage
GPUusageDecimal = 2                                                        # Number of decimal to be displayed.

GLOBAL_SBILL_DEFAULT_FORMAT = ['JobID','JobName%10','Account','Partition','NCPUS','NGPUS','Elapsed','State',Service]  # Default sbill format of your system
--------------

2. Copy sbill to a directory, such as /usr/local/bin 
--> cp sbill /usr/local/bin

3. In ~/.bashrc, prepend the path of the directory to the PATH environment variable  
--> vi .bashrc
--> export PATH=/usr/local/bin:${PATH} # (Last line of ~/.bashrc)

4. Try 'sbill -h' or 'sbill -V'

Note:
To hide the setup of your system, you could use cython to convert and compile sbill to an executable. 
For example, using python3.10, change Step 2 to
--> cython --embed -3 sbill
--> cc -O3 $(python3-config --includes) sbill.c -o sbill.exe $(python3-config --ldflags) -lpython3.10
--> cp sbill.exe /usr/local/sbill
