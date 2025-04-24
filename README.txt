The pipeline uses the reminho/human-glioblastoma-dataset from Kaggle, which contains scRNA-seq data. Ensure you have Kaggle API credentials set up for downloading via kagglehub.

Project Overview
This repository contains a pipeline for analyzing single-cell RNA sequencing (scRNA-seq) data from the human glioblastoma dataset using a Graph Neural Network (GNN) and bioinformatics tools. The pipeline performs data preprocessing, clustering, GNN-based classification, and biological interpretation of glioblastoma cell populations.

Pipeline Steps

Dependency Check: Verifies required Python packages (e.g., PyTorch, Scanpy, torch-geometric) and their versions.
Data Loading: Loads the glioblastoma scRNA-seq dataset (matrix.mtx, barcodes.tsv, genes.tsv) and maps Ensembl gene IDs to symbols using MyGeneInfo.

Preprocessing:
Creates an AnnData object using Scanpy.
Normalizes data, performs log transformation, and applies PCA for dimensionality reduction.
Clusters cells using the Leiden algorithm (10 clusters identified, labeled 0-9).
Feature Selection & Filtering:
Selects the top 800 highly variable genes.
Filters genes and cells based on minimum expression thresholds.

Graph Construction:
Builds a cell-cell graph using nearest neighbors.
Prepares data for GNN using PyTorch Geometric, with Leiden cluster labels as targets.

GNN Model:
Implements an ImprovedGNN with Graph Convolutional Networks (GCN), batch normalization, residual connections, and dropout.
Trains the model to classify cells into clusters, achieving a test accuracy of 94.31% and F1 score of 94.30%.

Visualization:
Generates a UMAP plot (umap_clusters.png) to visualize clusters (see below).
Plots training metrics (loss, accuracy, F1 score) and a confusion matrix.
Biological Analysis:
Identifies the top 10 highly variable genes (e.g., CHI3L1, HLA-DRA, GFAP).
Performs differential expression analysis using the Wilcoxon test, visualizing top genes per cluster (rank_genes_groups_leiden_de.png).

Key Outputs
UMAP Visualization: Shows 10 Leiden clusters (0-9) in a 2D UMAP space, highlighting distinct cell populations in glioblastoma.
Differential Expression: Ranks genes by significance for each cluster, identifying markers like CHI3L1 (cluster 0), GFAP (cluster 1), and PLP1 (cluster 2).

Model Performance: Final test accuracy of 94.31% and F1 score of 94.30% on the GNN classification task.

