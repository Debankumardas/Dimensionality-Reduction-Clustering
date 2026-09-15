# Dimensionality Reduction & Unsupervised Clustering

## Overview

This project applies dimensionality reduction and unsupervised machine learning techniques to discover hidden patterns and structures in high-dimensional numerical data.

The analysis focuses on Principal Component Analysis (PCA) and three clustering approaches:

- K-Means Clustering
- DBSCAN
- Hierarchical Clustering

The project evaluates how dimensionality reduction can simplify high-dimensional data while preserving important information and how different clustering algorithms identify groups within the data.

## Reproducibility

The project uses a Python virtual environment and a documented dependency file.

### Environment Setup

```powershell
py -3.12 -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt


---

### Step 3 — Add the final project results to README

Below the reproducibility section, add:

```markdown
## Key Results

| Analysis | Result |
|---|---|
| Original feature space | 561 features |
| PCA components retained | 102 |
| Variance retained | Approximately 95% |
| K-Means optimal k | 2 |
| K-Means Silhouette Score | 0.4154 |
| DBSCAN configuration | eps=20, min_samples=5 |
| DBSCAN clusters | 2 |
| DBSCAN noise | 159 observations (2.16%) |
| DBSCAN Silhouette Score | 0.4256 |
| Hierarchical clusters | 2 |
| Hierarchical Silhouette Score | 0.4150 |

### Interpretation

The analysis identified meaningful structure in the high-dimensional smartphone sensor data. K-Means produced a particularly interpretable separation between stationary and movement-related activities, while DBSCAN achieved the highest Silhouette Score among the evaluated configurations.

Known activity labels were used only for post-hoc interpretation and were not provided to the clustering algorithms.

## Dataset Citation

Reyes-Ortiz, J., Anguita, D., Ghio, A., Oneto, L., & Parra, X. (2013). Human Activity Recognition Using Smartphones [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C54S4K

Dataset source: UCI Machine Learning Repository — Human Activity Recognition Using Smartphones.

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
- Scipy

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