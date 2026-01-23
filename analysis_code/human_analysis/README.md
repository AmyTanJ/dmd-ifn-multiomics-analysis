# Human RNA-seq Analysis

This directory contains analysis pipelines and notebooks for **human RNA-seq datasets** used in cross-species Duchenne muscular dystrophy (DMD) studies.

The workflows include both bulk RNA-seq and single-nucleus RNA-seq analyses, focusing on immune- and muscle-related transcriptional programs relevant to DMD.

---

## Subdirectories

### `bulk_rnaseq/`
Scripts for human bulk RNA-seq preprocessing and differential expression analysis.

Main components:
- SRA download and FASTQ generation
- Quality control (FastQC)
- Read alignment using STAR
- Gene-level quantification with featureCounts
- Differential expression analysis using DESeq2

---

### `single_nucleus_rnaseq/`
Analysis workflows for human single-nucleus RNA-seq data.

Includes:
- Cell Ranger–based preprocessing for 10x Genomics data
- Scanpy-based filtering, normalization, and clustering
- Bootstrap analysis
- Pathway-level analysis

---

## Notes

- Raw sequencing data and large intermediate files are not stored in this repository.
- Reference genome builds and annotation versions should be documented for reproducibility.
