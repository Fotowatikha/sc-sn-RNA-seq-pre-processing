# sc-sn-RNA-seq-pre-processing

Now considering that the emergence of scRNA-seq techniques provides the framework to study gene expression variability in tissue of interest, the pre-processing of high dimensional RNA-seq data also becomes an important topic. To this day, droplet-based technologies remain the technique of choice when it comes to capturing and sequencing a large number of individual cells. This method essentially barcodes single cells and tags each transcript with a unique molecular identifier (UMI) within individual droplets, which can significantly increase the throughput up to 10,000 cells per analysis. However, this technique is not free of noise, and one must carefully pre-process the data before any unbiased downstream analysis can be caried out. 

**Here, I will provide you with all the necessary information on how to use the single-cell/nuclei pre-processing pipeline, either in your own environment or on the HPC cluster.**

## About

By consider the gene count matrices as the starting point after mapping reads to the reference, the major steps in this pre-processing is to: (1) Provide the user with quality control (QC) plots to gain insight on the overall quality of the cells prior to any extensive filtering; (2) Correcting the data from cell-free ambient RNA; (3) Extensive filtering to remove droplets that are unlikely to represent intact individual cells; (4) Removal of droplets that violate the assumption for containing one cell; (5) Provide the user with QC plots to gain insight on the quality of the data post-filtering.

## Download the pipeline files from GitHub

You can either [download the files for the pipeline](https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh) from my Github page or download it it by using the "Code button" on the Github page and import it using:
line below.
```sh
git clone "https://github.com/Fotowatikha/sc-sn-RNA-seq-pre-processing.git"
```

## Setup Conda environment

This pipeline is made to run on a Conda environment containing all the crucial packages for Python, Snakemake and R. Here, i assume that you already have Anaconda or Miniconda installed. In case you don’t have it yet, then follow the steps below:

**Anaconda/Miniconda3 installation**

1. [Download the Anaconda installer form the website](https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh) or get the latest version using the line below.
```sh
wget "https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh"
```

2. Now install accordingly:
```sh
 bash "Anaconda/Miniconda3-<version>-Linux-x86_64.sh"
```

3. Check if you installed correctly by calling the list of you installed packages and tools:
```sh
conda list 
```

4. (Optional) - If you have an older version, update the conda package manager to the latest version:
```sh
conda update -n base conda
```

**Setting up the environment for the pipeline**

1. Now with Conda installed and update it is time to setup the environment that is required for the pipeline.
To install the essential packages and tools, it is important to set your Conda channels in the following order:
```sh
conda config --add channels defaults
conda config --add channels GenomeDK
conda config --add channels r
conda config --add channels bioconda
conda config --add channels conda-forge
```

2. Note that the channels you added first end up in the bottom for lower priority. This is intentional!
Make sure that the these channels are the only ones active. If you have any other channels, you should first remove them as stated below:
```sh
conda config --remove channels <name of channel>
```

3. The requirements are provided in the "requirements.txt" that you downloaded form the Github page. Make a new environment and install all the packages:
```sh
conda create --name sc_sn_RNA_seq_pipeline --file requirements.txt
```

