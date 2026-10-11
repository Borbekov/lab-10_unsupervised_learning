# Lab 10: Unsupervised Learning

Practical exercises from ISLR (Introduction to Statistical Learning) Chapter 12, implemented in Python using sklearn, scipy, and the ISLP library.

## Overview

This lab covers methods for finding structure in data without a response variable — principal components analysis, matrix completion, K-means, and hierarchical clustering — applied to US crime statistics, cancer cell line gene expression, simulated data, and a healthy vs. diseased tissue gene expression dataset.

## Datasets

- **USArrests** — violent crime rates and urban population for the 50 US states (loaded via `statsmodels.datasets.get_rdataset`)
- **NCI60** — gene expression measurements (6,830 genes) for 64 cancer cell lines
- **Ch12Ex13.csv** — gene expression data with 1,000 genes for 40 tissue samples (20 healthy, 20 diseased)
- Simulated datasets for K-means and hierarchical clustering, including a 60-observation, 50-variable, three-class dataset

## Topics Covered

### Principal Components Analysis

- Standardizing variables with `StandardScaler` before `PCA`
- Loadings (`components_`) and principal component scores (`transform`)
- Biplots of the first two principal components
- Proportion of variance explained (`explained_variance_ratio_`) and cumulative PVE plots

### Matrix Completion

- Low-rank approximation of a data matrix via SVD (`np.linalg.svd`)
- Iterative algorithm for imputing missing values using a low-rank approximation
- Tracking the relative error and comparing imputed values to the true ones

### K-Means Clustering

- `sklearn.cluster.KMeans` on simulated data with a known cluster structure
- Effect of `K` on the resulting clusters
- Multiple random initializations (`n_init`) and the total within-cluster sum of squares (`inertia_`)

### Hierarchical Clustering

- `AgglomerativeClustering` with complete, average, and single linkage
- Building dendrograms with `ISLP.cluster.compute_linkage` and `scipy.cluster.hierarchy.dendrogram`
- Cutting the dendrogram with `cut_tree` by number of clusters or by height
- Scaling variables before clustering
- Correlation-based distance via a precomputed dissimilarity matrix

### NCI60 Data Example

- PCA on high-dimensional gene expression data and visualizing cancer types in PC score space
- Hierarchical clustering of the cell lines with different linkages and comparison to the true cancer types
- Comparing hierarchical clustering with K-means clustering
- Clustering on the first few principal component scores instead of the full data

## Model Evaluation

- PVE and cumulative PVE for choosing the number of principal components
- `pd.crosstab` for comparing cluster assignments with the true labels or with other clustering results
- Within-cluster sum of squares for comparing K-means runs

## Pipeline

- `sklearn.pipeline.Pipeline` combining `StandardScaler` with `AgglomerativeClustering` or `KMeans`
- `sklearn.metrics.pairwise_distances` for Euclidean and correlation-based dissimilarity matrices

## Exercises

- Manual K-means with `K = 2` on six observations: random initial labels, centroid computation, reassignment until convergence, and plotting the final clusters
- **USArrests**: showing that $1 - r_{ij}$ is proportional to the squared Euclidean distance after standardizing each observation
- **USArrests**: computing PVE with `explained_variance_ratio_` and directly from Equation 12.10
- **USArrests**: hierarchical clustering with complete linkage and Euclidean distance, cutting into three clusters, with and without scaling the variables, and comparing the results
- Simulated three-class data (60 × 50): PCA score plot, K-means with `K = 2, 3, 4`, K-means on the first two PC scores, and K-means after scaling
- **Ch12Ex13**: hierarchical clustering of the tissue samples with correlation-based distance and complete, average, and single linkage

## Technologies

- Python 3.12
- scikit-learn
- scipy
- statsmodels
- ISLP
- pandas, numpy
- matplotlib
