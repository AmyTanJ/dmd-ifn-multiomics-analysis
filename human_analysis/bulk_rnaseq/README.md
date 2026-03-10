# 💾 Bulk RNA-seq pipeline (human DMD)

Bash and R scripts for human bulk RNA-seq from SRA to differential expression (DMD vs Healthy): download, QC, alignment with STAR, gene counting with featureCounts, and DESeq2.  
Part of [human_analysis](../README.md) (see also single-nucleus RNA-seq).

## 📁 Pipeline overview

| Script | Purpose | Main input | Main output |
|--------|---------|------------|-------------|
| **download_sra.sh** | Download SRA runs with prefetch | SRR accessions (edit in script) | `.sra` under `./humanDMD/2nd_DMD/SRA` |
| **convert_sra_to_fastq.sh** | SRA → paired FASTQ + manifest | `.sra` files | `*_R1.fastq.gz`, `*_R2.fastq.gz`, `samples_manifest.tsv` |
| **run_fastqc.sh** | FastQC (and MultiQC if installed) | FASTQ directory | `FASTQ/QC/`, `multiqc_report.html` |
| **build_star_index.sh** | Build STAR genome index | FASTA + GTF | `./humanDMD/ref/STAR_GRCh38_gencodev39` |
| **align_star.sh** | Align reads, sort BAM, index | `samples_manifest.tsv`, STAR index | `*_Aligned.sortedByCoord.out.bam` |
| **count_features_featurecounts.sh** | Gene-level counts | BAMs + GTF | `gene_counts.matrix.txt` |
| **differential_expression_deseq2.R** | DESeq2 DMD vs Healthy | `gene_counts.matrix.txt` | PCA/MA plots, results in `DE_ifna_results/` |

## 🔗 Run order

1. **download_sra.sh**  
2. **convert_sra_to_fastq.sh**  
3. **run_fastqc.sh** (optional but recommended)  
4. **build_star_index.sh** (once per reference)  
5. **align_star.sh**  
6. **count_features_featurecounts.sh**  
7. **differential_expression_deseq2.R**  

## 🧰 Prerequisites

- **SRA Toolkit**: `prefetch`, `fasterq-dump`  
- **FastQC**, optional **MultiQC** (`pip install multiqc`)  
- **STAR** (alignment)  
- **samtools** (BAM index)  
- **subread** (`featureCounts`)  
- **pigz** (compression)  
- **R** with: DESeq2, tidyverse, org.Hs.eg.db, ReactomePA, msigdbr, glue, readr  

## 📂 Paths

Scripts use example paths under `./humanDMD/` (e.g. `./humanDMD/ref/`, `./humanDMD/2nd_DMD/`). Place your reference FASTA and GTF in `./humanDMD/ref/` or set the variables at the top of each script to match your layout.

## 📚 Reference

- **Human bulk RNA-seq data**: Nieves-Rodriguez et al., Frontiers in Genetics 2023, “Transcriptomic analysis of paired healthy human skeletal muscles to identify modulators of disease severity in DMD” ([https://www.frontiersin.org/journals/genetics/articles/10.3389/fgene.2023.1216066/full](https://www.frontiersin.org/journals/genetics/articles/10.3389/fgene.2023.1216066/full)).

