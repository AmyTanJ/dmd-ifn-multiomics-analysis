# 🧯 IFNAR1 chimeras: label transfer, pseudo-bulk matching, and scSemiProfiler deconvolution

Analysis code for diaphragm macrophage experiments in **Ifnar1-/- Donor/mdxHost** and **Ifnar1+/+ Donor/mdxHost** chimeras. This folder contains notebooks to (1) transfer labels from the mouse sex-chimeric single-cell reference, (2) match bulk RNA-seq samples to pseudo-bulk profiles, and (3) run single-cell–level deconvolution with **scSemiProfiler**.

## 📁 Contents

| Notebook | Description |
|----------|-------------|
| **label_transfer.ipynb** | Use the sex-chimeric macrophage single-cell dataset as a reference, preprocess chimeric single-cell data with the same QC/normalization, and run `scanpy.tl.ingest` to transfer cluster labels and project chimeric cells into the reference UMAP/clustering space. |
| **pseudobulk_analysis.ipynb** | Build normalized pseudo-bulk profiles from sex-chimeric single-cell data, normalize chimeric bulk RNA-seq, and compute Pearson/cosine similarity to identify the best-matching bulk reference sample for each condition. |
| **semiprofiler_analysis.ipynb** | Follow the bulk-deconvolution tutorial from [scSemiProfiler](https://github.com/mcgilldinglab/scSemiProfiler) using the pseudo-bulk–selected representative bulk sample and the sex-chimeric single-cell reference to infer target single-cell profiles for the chimeras, then train a classifier on the reference to annotate inferred cells. |

## 🔗 Run order (high level)

1. **label_transfer.ipynb** – Confirm cell-type/cluster annotations in the sex-chimeric reference and transfer them onto chimeric single-cell data for plotting and QC.
2. **pseudobulk_analysis.ipynb** – Generate pseudo-bulk profiles from the sex-chimeric reference and select the bulk sample with highest similarity for each condition.
3. **semiprofiler_analysis.ipynb** – Use the selected bulk reference and sex-chimeric single-cell reference in **scSemiProfiler** to deconvolute chimeric bulk RNA-seq into single-cell data and perform cell-type annotation.

## 🧰 Prerequisites

- **Inputs**
  - Sex-chimeric macrophage single-cell dataset saved as `.h5ad` (reference).
  - Single-cell RNA-seq for Ifnar1-/- Donor/mdxHost and Ifnar1+/+ Donor/mdxHost chimeras.
  - Bulk RNA-seq count matrix for the same chimeras (and the sex-chimeric reference) saved as `.h5ad` for scSemiProfiler.

- **Environment**
  - Python with: **scanpy**, **anndata**, **numpy**, **pandas**, **matplotlib**, **seaborn**, **scrublet**, **scSemiProfiler** (see [scSemiProfiler installation instructions](https://github.com/mcgilldinglab/scSemiProfiler)), and **scipy**.

Paths in the notebooks assume the current project layout (e.g. `./deconvolution_CD451_10/`, `./Bulk_Rna_CD45_1_filtered.h5ad`); adjust them if your data are stored elsewhere.

