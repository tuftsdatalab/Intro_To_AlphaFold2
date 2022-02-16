30 minutes

## Log into the HPC cluster’s On Demand Interface

- Open a Chrome browser and go to [On Demand](https://ondemand.pax.tufts.edu/)
- Log in with your Tufts Credentials
- On the top menu bar choose `Clusters->Tufts HPC Shell Access`

![](images/shell.PNG)

- You'll see a welcome message and a bash prompt, for example for user `tutln01`:

|`[tutln01@login001 ~]$`|
|-|

This indicates you are logged in to the login node of the cluster.

## How Should We Run AlphaFold2?

Now that we are at a login node we need to get to a compute node to get our job done. For shorter jobs we can get an interactive session like so:

|DO NOT RUN|
|--|
|`srun --pty -t 3:00:00 --mem 16G -N 1 --cpus 4 bash`|

Where:

|`srun`|SLURM command to run a parallel job|
|-|-|
|`--pty`| get a pseudo terminal|
|`-t` | time we need here we request 3 hours|
|`--mem` | memory we need here we request 16 Gigabytes|
|`-N` | number of nodes needed here we requested 1 node|
|`--cpus` | number of CPUs needed here we requested 4|

However, a program like AlphaFold might take much longer and require more memory than we can request in an interactive session like this. So to run our job we will need to write a batch script. A batch script will allow us to submit our job to a queue to be run on a compute node. The following graphic shows which solution is the best fit given the size of the job:

![](images/srun_v_sbatch.PNG)

## Prepare the Batch Script
```
#!/bin/bash
#SBATCH -p preempt  #if you don't have ccgpu access, use "preempt"
#SBATCH -n 8    # 8 cpu cores
#SBATCH --mem=64g       #64GB of RAM
#SBATCH --time=2-0      #run 2 days, up to 7 days "7-00:00:00"
#SBATCH -o output.%j
#SBATCH -e error.%j
#SBATCH -N 1
#SBATCH --gres=gpu:1    # number of GPUs. please follow instructions in Pax User Guidewhen submit jobs to different partition and selecting different GPU architectures.
#SBATCH --exclude=c1cmp[025-026] #avoid using K20xm

module load alphafold/2.1.1
nvidia-smi
module help alphafold/2.1.1 
#this command will print out all input options for "runaf2"command
#Please use your own path/value for the following variables
#Make sure to specify the outputpath to a path that you have write permission
mkdir /cluster/home/jlaird01/alphaFoldTest/afTest2
outputpath=/cluster/home/jlaird01/alphaFoldTest/afTest2
fastapath=/cluster/home/jlaird01/alphaFoldTest/hsp90.fasta
maxtemplatedate=2020-06-10
source activate alphafold2.1.1
#running alphafold 2.1.1
runaf2 -o $outputpath -f $fastapath -t $maxtemplatedate
```
_________________________________________________________________________________________________________________________________________________________________________________

Next Lesson: [AlphaFold2 Output](../lesson3/lesson3.md)

Previous: [Introduction to AlphaFold2](../lesson1/AlphaFold2_Tutorial.pdf)
