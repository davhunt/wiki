---
layout: default
title: Job Submission
parent: HPC
nav_order: 3
---

### Contents
1. [Overview](#overview)
2. [Creating a Slurm File](#creating-a-slurm-file)
3. [Running a Slurm File](#running-a-slurm-file)
4. [Why is my job taking forever?](#why-is-my-job-taking-forever)

## Overview
For anything that goes beyond running basic lines of code, a job must be submitted to the compute nodes so that the compute nodes can properly handle tasks. Note, this is a **requirement** on the HPC, as login nodes are not the intended resource for computation.

## Creating a Slurm File
To create a job, a [slurm](https://slurm.schedmd.com/documentation.html) file must be created:
1. Your script (.R, .py, .m, etc.) should already be created (in the `code` folder of your project) and you should have already bug-tested this script on your local machine. Push it to your project repository on GitHub and merge it to the `main` branch.
2. Make sure that you are connected to the FIU VPN using your personal credentials. Follow the instructions [here](https://fiu.service-now.com/sp?id=kb_article&sys_id=6c3c789ddb899780b16af969af96193d).
3. Using Google Chrome as your browser, visit [hpcgui.fiu.edu](hpcgui.fiu.edu) and log in with your personal credentials.
4. Under Clusters, select "Panther Shell Access."
![shell-access](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/shell-access.png)
5. When prompted, input your password. (It will no look like you are typing anything, but persevere and hit Enter!)
6. Navigate, using `cd` commands, to the folder where your script lives. This is where you will want to place the slurm file.
7. If a nightly sync has not already taken place, manually sync this folder to the GitHub remote with the command `git pull`.
8. Create and open a new file with the command `nano USEFULNAME.sub` where USEFULNAME is replaced by an actually useful name that describes what this .sub file will do.
9. Type or paste into the empty file the necessary script information. See below for an example that can be customized.
10. Save your new file by holding down the ctrl key and pressing the letter 'o'. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return.
11. To exit the nano view, hold down the ctrl key again and press the letter 'x'.
12. Use `ls` to inspect the contents of the folder. You should see your new .sub file.

The file below represents a sample Slurm script where a conda base environment is being activated: 

```yml
#!/bin/bash

#SBATCH --job-name=myjob         	# job name
#SBATCH --nodes=1                	# node count
#SBATCH --ntasks=1               	# total number of tasks across all nodes
#SBATCH --time=00:10:00          	# total run time limit (HH:MM:SS)
#SBATCH --account=iacc_gbuzzell		# SLURM account name (delete this line if not running a highmem job)
#SBATCH --mail-type=end          	# send email when job ends

module load singularity-3.8.2

singularity exec --bind /home/data/NDClab /home/data/NDClab/tools/containers/python-3.8/python-3.8.simg python3 filename.py
```

Here is a guide to what these details in the .sub file mean and how they should be customized:

| variable/text  | description  | how to customize  |
| :--  | :--  | :--  |
| #!/bin/bash  | tells the HPC to read what follows in the Bash language  | Do not modify.  |
| job-name  | name for the job that displays in squeue  | Replace "myjob" with a short, informative name for the job you are running. You can then see this easily on the squeue.  |
| nodes  | tells the HPC how many nodes should be utilized (nodes are individual computers in the cluster)  | Keep at "1" unless you are doing parallel processing.  |
| tasks  | tells the HPC how many tasks (that is, CPUs) should be utilized across the number of nodes selected | Keep at "1" unless you are doing parallel processing.  |
| time  | limits the amount of time the HPC should devote to running the script  | Ballpark the time your script will need to run and give yourself some buffer. For parallel processes, this will need to be set very high. But be careful not to burn through lab time on the HPC.  |
| account | The HPC account used to run the script | By default this will be "acc_gbuzzell" and this line can be omitted. For high memory jobs, "iacc_gbuzzell" should be used. |
| mail-type  | tells the HPC to send you an e-mail when the job is done  | If the job is very small and will run quickly, you can delete this line to avoid an unnecessary e-mail in your inbox. Otherwise, leave it unchanged.  |
| module load singularity-3.8.2  | loads the IRCC-managed singularity image  | Do not modify. (However, if you become aware of a newer image, please PR a suggested wiki update to the lab technician!)  |
| singularity exec --bind /home/data/NDClab  | binds data within the NDCLab folder to the singularity image  | Do not modify.  |
| /home/data/NDClab/tools/containers/python-3.8/python-3.8.simg  | identity of the selected container  | Use the example for Python. For R, use `/home/data/NDClab/tools/containers/R/R-4.2.2A/R-4.2.2A.simg`  |
| python3 filename.py  | the actual command to run the script specified  | Specify python3 for .py or Rscript for .R.  |

MATLAB is a little special. To create a Slurm script for a .m file, replace the `singularity` line in the sample above with:
```yml
module load matlab-2018b
matlab -nodisplay -nosplash -r filename
```
...where `filename` is the name of your MATLAB script, but without the final `.m`.


## Running a Slurm File
To run an existing slurm file, you will log into the HPC and utilize the [shell](https://ndclab.github.io/wiki/docs/technical-docs/shell.html) interface to execute the script.
1. First, make sure that you are connected to the FIU VPN using your personal credentials. Follow the instructions [here](https://fiu.service-now.com/sp?id=kb_article&sys_id=6c3c789ddb899780b16af969af96193d).
2. Using Google Chrome as your browser, visit [hpcgui.fiu.edu](hpcgui.fiu.edu) and log in with your personal credentials.
3. Under Clusters, select "Panther Shell Access."
![shell-access](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/shell-access.png)
4. When prompted, input your password. (It will no look like you are typing anything, but persevere and hit Enter!)
5. Navigate to the folder containing the slurm file (file extension `.sub`) that you want to execute using `cd` commands.
6. Run the script by typing the following into the shell: `sbatch <filename.sub>`. For instance, to execute a hallMonitor.sub file, you would type `sbatch hallMonitor.sub`.
7. The shell will output a message to indicate that the batch was submitted and its associated job number:
![sbatch-submit](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/sbatch-submit.png)
8. Check status and runtime of currently running scripts with the squeue command: `squeue -u <username>`.
9. Use `ls` to see if the process is complete. When it is complete, you will see an output file in the same folder whose name is "slurm-NUMBER.out":
![sbatch-output](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/sbatch-output.png)
10. Use `cat slurm-NUMBERS.out` to print all messages to the console.
11. If your script is designed to output any new files (for example, a CSV), and assuming you don't get any error messages, that file should now exist in the appropriate folder.

## Why is my job taking forever?

The batch scheduler submits jobs to the HPC based on the order in which they're received, as well as the requested memory allocated, requested walltime, and how many other jobs are currently running. To check on the status of your jobs you can use squeue, `squeue -u <username>`, where you will see your submitted jobs along with how long they've been running and their status (PD=pending, R=running).

If your jobs are sitting in the queue for longer than you would like, you can check on how busy the HPC is with the `sar` command. A %idle of ~60 or less indicates that the HPC is very busy and may not get to your jobs for a while, especially if they're large memory or long walltime jobs. If you think your job can afford to be submitted with less memory or walltime, you can try cancelling `scancel NUMBERS` and resubmitting the job with fewer resources requested.
