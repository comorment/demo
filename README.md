# Docker and Singularity containers for GWAS analysis 

A Hello World Singularity container, which you may use to familiraze yourself with Singularity infrastructure of your secure HPC environment (TSD, Bianca, Computerome, or similar).
This singularity container is indented as a demo, and contains only Plink 1.9 (http://zzz.bwh.harvard.edu/plink/) software.
We are currently working on expanding the container to include a lot of additional software used for GWAS and post-GWAS analysis.

## Getting Started

Download ``hello_v1.0.sif`` and ``hello_demo.tar.gz`` files from https://drive.google.com/drive/folders/1mfxZJ-7A-4lDlCkarUCxEf2hBIxQGO69?usp=sharing
Import these files to your secure HPC environment (i.e. TSD, Bianca, Computerome, or similar).
Run ``tar -xzvf hello_demo.tar.gz`` to extract demo data.

Run ``singularity exec --no-home hello_v1.0.sif plink --help``, to validate that you can run singularity interactively.
Run ``singularity exec --no-home -B $(pwd):/data hello_v1.0.sif plink --bfile /data/chr21 --freq --out /data/chr21``, to mount current folder into container under ``/data``, and use plink to calculate allele frequencies
Run ``singularity shell --no-home -B $(pwd):/data hello_v1.0.sif`` to use singularity in an interactive mode.
Run singularity container within SLURM job scheduler, by creating a ``hello_slurm.sh`` file (by adjusting an example below), and running ``sbatch hello_slurm.sh``.

```
#!/bin/bash
#SBATCH --job-name=hello
#SBATCH --account=p697
#SBATCH --time=00:10:00
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=8000M
module load singularity/2.6.1
#singularity exec --no-home hello_v1.0.sif plink --help
singularity exec --no-home -B $(pwd):/data hello_v1.0.sif plink --bfile /data/chr21 --freq --out /data/chr21
```

For the both alternatives, you should observe the welcome page of plink starting with:

```
PLINK v1.90b6.18 64-bit (16 Jun 2020)          www.cog-genomics.org/plink/1.9/
(C) 2005-2020 Shaun Purcell, Christopher Chang   GNU General Public License v3

In the command line flag definitions that follow............
```
