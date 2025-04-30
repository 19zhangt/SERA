## SERA - a computational framework for analyzing multiple RNA-based phenotypes in scRNA-seq data

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)  [![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)  [![R 4.2.2](https://img.shields.io/badge/R-4.2.2-blue)](https://www.r-project.org/)

<p align="center"><img  src="assets/SERA.png" width="60%" /></p>

Currently, **SERA** quantitively analyzed three such phenotypes: gene expression, APA, and RNA editing at a population scale using polyA-enriched single-cell RNA-sequencing data. With its efficient design, **SERA** helps researchers uncover insights into RNA processing, and cellular heterogeneity, offering a comprehensive view of transcriptional diversity at the single-cell level.

**Key Features**:

- **Single-cell resolution**: work with polyA-enriched single-cell RNA-seq data.
- **Multimodal post-transcriptional modification**: capable of identifying multiple post-transcriptional modification types.
- **Population-scale analysis**: scalable to large datasets, enabling population-level studies of transcriptional phenotypes.

---
## Table of Contents
- [Installation](#installation-)
- [Quick Start](#quick-start-)
- [Data Requirements](#data-requirements-)
- [Output](#output-)


## Installation 🔧

1. Clone this repository:
   ```bash
   git clone https://github.com/lilab-bioinfo/SERA.git
   cd SERA
   ```

2. Install dependency with mamba
   ```bash
   conda install -n base mamba
   mamba env create -f environment.yml
   conda activate SERA
   ```

## Quick Start 🚀

**SERA** provides a command-line interface (CLI) for ease of use. Below is a basic example of how to analyze single-cell RNA-seq data.

### For gene expression
```bash
Rscript SERA.R --mode expression \
  --cellinfo example/cell_annotation.csv \
  --baminfo example/bam_list.csv \
  --threads 50 \
  --outdir example/output
```

### For poly(A) sites and alternative polyadenylation events
```bash
Rscript SERA.R --mode apa \
  --cellinfo example/cell_annotation.csv \
  --baminfo example/bam_list.csv \
  --genome_fa xxx/hg38/genome.fa \
  --threads 50 \
  --outdir example/output
```

### For RNA editing sites
```bash
Rscript SERA.R --mode editing \
  --cellinfo example/cell_annotation.csv \
  --baminfo example/bam_list.csv \
  --genome_fa xxx/hg38/genome.fa \
  --py2_path /usr/bin/python2 \
  --threads 50 \
  --outdir example/output
```

### For all phenotypes
```bash
Rscript SERA.R --mode all \
  --cellinfo example/cell_annotation.csv \
  --baminfo example/bam_list.csv \
  --genome_fa xxx/hg38/genome.fa \
  --py2_path /usr/bin/python2 \
  --threads 50 \
  --outdir example/output
```

## Data Requirements 📂

SERA starts with the outputs from **cellranger**, user need to specify two parameters for SERA

- `--mode`: Specify the analysis mode (`expression`, `apa`, `editing`, `all`).
- `--cellinfo`: path to the cell information table in CSV format, containing four columns with the following column names: `pool`, `barcode`, `cell_type`, `donor`, such as:
  ```text
  pool,barcode,cell_type,donor
  S1,AAACCCACACCATTCC-1,CD4,ind1
  S1,AAACCCACATCCGATA-1,CD8,ind2
  S2,AAACCCATCTCTGCTG-1,NK,ind3
  S2,AAACGAACATTGAGGG-1,Mono,ind4
  ```

- `--baminfo`: the output directory of cellranger bam files.
  ```text
  pool,bamfile
  S1,data/cellranger/S1/outs/possorted_genome_bam.bam
  S2,data/cellranger/S2/outs/possorted_genome_bam.bam
  ```

- `--genome_fa`: genome sequence file in fasta format.
- `--outdir`: Path to the output directory where results will be saved.


## Output 🖨️

The results will be saved in the specified output directory, and they include matrix of multimodal molecular phenotypes for each cell type, where the columns represent sample IDs and the rows represent phenotype names.

- Normalized gene expression
- poly(A) sites and APA usage matrices
- RNA editing sites and RNA editing levels


## Getting help 📬

If you encounter a bug or have a feature request, please open an [Issues](https://github.com/lilab-bioinfo/SERA/issues).

If you would like to discuss questions related to single-cell analysis, you can open a [Discussions](https://github.com/lilab-bioinfo/SERA/discussions).


## Release Notes​​ 🎉

v1.0.0 (2025-04-21): Initial release with analysis pipeline

---