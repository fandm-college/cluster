---
title: Introduction - Slurm job scheduler
layout: page
nav_order: 3
---

# Overview

Running programs on the cluster is different from how you might typically run software on your personal computer.  The cluster uses a software package called Slurm 
(**S**imple **l**inux **u**tility for **r**esource **m**anagement) to manage how/when programs are run on the cluster.  Essentially, you will submit a job request to run your software with certain computational resources.  Your request will be placed in a job queue and remain there until 

1. Your job gets to (or near) the front of the queue AND 
2. All necessary resources (e.g. # of CPUs, memory, etc.) that your job needs to run are available.

# Example job request

```bash
#!/bin/bash

#SBATCH --job-name=sample_chemistry-job
#SBATCH --output=chem.out
#SBATCH --ntasks=16
#SBATCH --ntasks-per-node=4
#SBATCH --mem=12G
#SBATCH --mail-type=BEGIN,END,FAIL
#SBATCH --mail-user=auser@fandm.edu

# Load the software package we want to use
module purge
module load mychemistrysoftware

computeChemistry inputFile.txt
```

Above is a very simple, but typical, job request file.  There are essentially three sections to this and any job request:

1. `#!/bin/bash`
    - This must be in all job requests and must be the first line
2. Job scheduler directives denoted by `#SBATCH`.  These provide information to the job scheduler such as
    - Name of the job
    - Output file anything that would normally print to the screen
    - Computational resources being requested(types, amounts, etc.)
    - Other information used by the scheduler
3. All commands needed to actually perform the computation
    - Loading the software for use
    - Running the software
    - Any other commands (e.g., move/copy data)

This example only uses one software application one time, but a job request might

    - Use the same software application package several times and/or
    - Use multiple software applications

# Choosing compute resources

The choice of resources, especially resource amounts is strongly dependent on the softwre application(s) you use and 
the workflow you have in place for your research.