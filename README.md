gifrop examples
================

# Install gifrop

Make sure you have some kinda of conda installation completed. I like
miniconda.  
<https://www.docs.conda.io/en/latest/miniconda.html>

Once you have miniconda install gifrop.

From the command line:

``` bash
conda create -n gifrop
conda activate gifrop
conda install -c conda-forge -c bioconda -c defaults gifrop

# Test that gifrop was installed correctly

gifrop --help
pan_pipe --help
```

# Clone test repo

If you want to follow along you can clone the repo I’ll be working from.

``` bash
git clone https://www.github.com/jtrachsel/gifrop_examples.git  
cd gifrop_examples
```

# First Test

  - Two strains of Salmonella enterica
      - LT2: famous reference strain  
      - USDA15WA-1: Isolate under investigation in the Bearson Lab

Two genomic islands of interest here. 80kb metal tolerance island
(SGI4), 28kb multidrug resist module.

For this example I have already annotated the genomes with prokka and
generated the pangenome with Roary.

Show gene\_presence\_absence.csv

``` bash
cd test1

cd pan

gifrop --get_islands --threads 8  

cd gifrop_out

ls

cd ../../..
```

Show clustered island info, explain columns. Show gpa\_clust.  
Show secondary cluster heatmap.

Identified 80kb metal island, 28kb MDR module, phage etc.  
\- show extracted fasta and gff.

# Test 2

Campylobacter draft genomes from an AMR transfer experiment.  
1\. C. coli donor Tet resistant  
2\. C. jejuni recipient Tet sensitive  
3\. C. jejuni result Tet resistant

``` bash
cd test2

ls

# takes ~7 minutes
pan_pipe --prokka_args '--cpus 2' --roary_args '-p 8' --gifrop_args '--threads 8'

# pan_pipe --prokka_args '--cpus 24' --roary_args '-p 60' --gifrop_args '--threads 60'

cd pan

cd gifrop_out

ls

cd ../../../
```

Show secondary cluster by genome. Show transfered tet resistance island.

# Test 3

A messy dataset. Should show some of the main problems with this
approach.

7 Salmonella strains.

I precomputed these results for the sake of time.

``` bash

pan_pipe --prokka_args '--cpus 2 --proteins LT2.gbk' --roary_args '-p 8' --gifrop_args '--threads 8'

# takes ~ 7 minutes
```

Look at clustered island info, try and find MDR and SGI4.

Look at secondary cluster by genome heatmap.  
Look at secondary cluster 132? heatmap, show problems.  
Look at clustering graph.

Potential solutions:

  - Do some pruning on the clustering graph before community
    identification.
      - remove low weight edges?
          - remove edges of weight 1  
          - calculate a median edge weight for each primary cluster  
          - remove edges weighted less than 1/4 of median edge weight?
