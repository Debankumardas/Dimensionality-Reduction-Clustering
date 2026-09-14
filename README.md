# Dimensionality Reduction & Unsupervised Clustering

## Overview

This project applies dimensionality reduction and unsupervised machine learning techniques to discover hidden patterns and structures in high-dimensional numerical data.

The analysis focuses on Principal Component Analysis (PCA) and three clustering approaches:

- K-Means Clustering
- DBSCAN
- Hierarchical Clustering

The project evaluates how dimensionality reduction can simplify high-dimensional data while preserving important information and how different clustering algorithms identify groups within the data.

## Objectives

- Standardize high-dimensional numerical features.
- Apply Principal Component Analysis (PCA).
- Analyze explained variance using scree and cumulative variance plots.
- Determine an appropriate number of principal components.
- Apply K-Means clustering.
- Determine the optimal number of clusters using the Elbow Method and Silhouette Score.
- Apply DBSCAN clustering and analyze its parameters.
- Apply Hierarchical Clustering.
- Visualize clusters using 2D and 3D PCA projections.
- Compare the clustering behavior of different algorithms.

## Methodology

The project follows the following workflow:

1. Dataset acquisition and documentation
2. Data loading and exploratory inspection
3. Data quality checks
4. Feature selection
5. Feature standardization
6. Principal Component Analysis
7. Explained variance analysis
8. K-Means clustering
9. Elbow Method analysis
10. Silhouette Score analysis
11. DBSCAN clustering
12. Hierarchical clustering
13. 2D and 3D cluster visualization
14. Clustering comparison
15. Final interpretation

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Plotly
- Jupyter Notebook

## Project Structure

```text
Dimensionality-Reduction-Clustering/
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│
├── notebooks/
├── reports/
├── src/
├── tests/
│
├── README.md
├── .gitignore
└── requirements.txt