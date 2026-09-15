# Dimensionality Reduction & Unsupervised Clustering

An end-to-end unsupervised machine learning project exploring whether **Principal Component Analysis (PCA)** and multiple clustering algorithms can reveal meaningful activity patterns in high-dimensional smartphone sensor data.

---

## Project Overview

High-dimensional datasets can contain hundreds of features, making analysis, visualization, and clustering difficult.

This project applies a reproducible dimensionality-reduction and unsupervised-learning pipeline to the **UCI Human Activity Recognition Using Smartphones** dataset.

The analysis focuses on:

* Feature standardization
* Principal Component Analysis (PCA)
* Explained variance analysis
* K-Means clustering
* Elbow Method
* Silhouette Score
* DBSCAN clustering
* Hierarchical clustering
* Dendrogram analysis
* 2D and 3D cluster visualization
* Internal clustering evaluation
* Post-hoc activity interpretation

### Research Question

> **Can PCA and unsupervised clustering reveal meaningful activity patterns in high-dimensional smartphone sensor data?**

---

## Dataset

This project uses the **Human Activity Recognition Using Smartphones** dataset from the UCI Machine Learning Repository.

### Dataset Characteristics

| Property           |                                        Value |
| ------------------ | -------------------------------------------: |
| Dataset            | Human Activity Recognition Using Smartphones |
| Instances          |                                       10,299 |
| Numerical features |                                          561 |
| Subjects           |                                           30 |
| Activities         |                                            6 |
| Missing values     |                                         None |
| Sampling frequency |                                        50 Hz |
| Sensor             |                          Samsung Galaxy S II |
| Data type          |                     Multivariate time-series |

### Activities

The dataset contains six predefined activities:

1. WALKING
2. WALKING_UPSTAIRS
3. WALKING_DOWNSTAIRS
4. SITTING
5. STANDING
6. LAYING

**Important:** The activity labels were not supplied to the clustering algorithms. They were used only after clustering for post-hoc interpretation.

### Dataset Source

UCI Machine Learning Repository:

Human Activity Recognition Using Smartphones

https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones

---

## Project Workflow

```text
UCI HAR Dataset
       │
       ▼
Data Loading & Validation
       │
       ▼
Feature Name Cleaning
       │
       ▼
Standardization
(StandardScaler)
       │
       ▼
Principal Component Analysis
(PCA)
       │
       ▼
~95% Variance Retained
       │
       ▼
102 Principal Components
       │
       ├───────────────┐
       ▼               ▼
   K-Means          DBSCAN
       │               │
       ▼               ▼
Elbow Method      Parameter Search
Silhouette Score  Noise Analysis
       │               │
       └───────┬───────┘
               ▼
      Hierarchical Clustering
               │
               ▼
       Model Comparison
               │
               ▼
       Cluster Visualization
               │
               ▼
    Post-Hoc Interpretation
```

---

## Methodology

### 1. Data Loading

The training and testing feature matrices were loaded from the original UCI dataset.

* Training observations: **7,352**
* Test observations: **2,947**
* Features: **561**

The original train/test separation was preserved.

---

### 2. Data Validation

The dataset was checked for:

* Correct dimensions
* Missing values
* Duplicate feature names
* Feature consistency
* Numerical data types

The UCI dataset contains duplicate feature names in `features.txt`. These were resolved by adding unique suffixes while preserving all 561 original features.

---

### 3. Feature Standardization

Because the sensor-derived features operate on different scales, the numerical features were standardized using:

```python
StandardScaler()
```

The scaler was fitted only on the training data and then applied to the test data.

This prevents information from the test set from influencing the training transformation.

---

## Principal Component Analysis

PCA was applied after standardization to reduce the dimensionality of the dataset.

The original feature space contained:

```text
561 features
```

The selected PCA representation contains:

```text
102 principal components
```

while retaining approximately:

```text
95% of the original variance
```

### PCA Results

| Metric                | Result |
| --------------------- | -----: |
| Original dimensions   |    561 |
| Selected components   |    102 |
| Variance retained     |   ~95% |
| Training observations |  7,352 |
| Test observations     |  2,947 |

The PCA scree plot and cumulative explained variance analysis are included in the notebook.

---

## K-Means Clustering

K-Means clustering was evaluated for:

```text
k = 2 to 10
```

Two approaches were used to determine an appropriate number of clusters.

### Elbow Method

The Elbow Method was used to examine how K-Means inertia decreases as the number of clusters increases.

### Silhouette Score

The Silhouette Score was also calculated for each candidate value of `k`.

The highest Silhouette Score was obtained at:

```text
k = 2
```

### K-Means Result

```text
Optimal k: 2
Silhouette Score: 0.4154
```

The two-cluster solution revealed a meaningful broad separation between stationary and movement-related observations.

---

## DBSCAN Clustering

DBSCAN was evaluated using multiple `eps` values while keeping:

```text
min_samples = 5
```

The tested values included:

```text
eps = 3, 5, 7, 10, 15, 20
```

The selected configuration was:

```text
eps = 20
min_samples = 5
```

### DBSCAN Result

| Metric             |     Result |
| ------------------ | ---------: |
| Clusters           |          2 |
| Noise observations |        159 |
| Noise percentage   |      2.16% |
| Silhouette Score   | **0.4256** |

DBSCAN produced the highest Silhouette Score among the evaluated clustering configurations.

---

## Hierarchical Clustering

Agglomerative Hierarchical Clustering was applied using:

```text
n_clusters = 2
linkage = "ward"
```

### Result

```text
Clusters: 2
Silhouette Score: 0.4150
```

A dendrogram was generated using a representative sample of 300 observations to make the hierarchical structure easier to interpret.

---

## Clustering Model Comparison

The three clustering approaches were evaluated using internal validation metrics.

| Method       | Configuration         | Clusters | Noise | Silhouette Score |
| ------------ | --------------------- | -------: | ----: | ---------------: |
| K-Means      | k=2                   |        2 |     0 |           0.4154 |
| DBSCAN       | eps=20, min_samples=5 |        2 |   159 |       **0.4256** |
| Hierarchical | 2 clusters, Ward      |        2 |     0 |           0.4150 |

Additional evaluation metrics, including:

* Calinski-Harabasz Score
* Davies-Bouldin Score

are calculated in the notebook.

### Best Internal Result

Based on the Silhouette Score:

```text
DBSCAN
Silhouette Score = 0.4256
```

Therefore, DBSCAN provides the strongest internal clustering result among the evaluated configurations.

However, K-Means provides a particularly clear and interpretable broad separation of the activity patterns.

---

## Post-Hoc Activity Interpretation

The known activity labels were deliberately excluded from the clustering process.

After clustering, the labels were used only to understand what the discovered clusters represented.

The K-Means results showed a strong broad separation between:

### Stationary Activities

* LAYING
* SITTING
* STANDING

### Movement-Related Activities

* WALKING
* WALKING_UPSTAIRS
* WALKING_DOWNSTAIRS

This indicates that unsupervised learning was able to discover meaningful structure in the sensor data without directly using the known activity labels.

The clusters should **not** be interpreted as exact replacements for the six predefined activity classes. Instead, they represent patterns discovered by the unsupervised algorithms.

---

## Visualizations

The project includes several visual analyses.

### PCA

* Explained Variance Ratio
* Cumulative Explained Variance
* PCA scree plot

### K-Means

* Elbow Method
* Silhouette analysis
* 2D PCA cluster projection
* Cluster centroid visualization

### DBSCAN

* Parameter evaluation
* Noise analysis
* 2D PCA cluster visualization

### Hierarchical Clustering

* Dendrogram
* 2D PCA cluster projection

### Overall

* Cluster-size comparison
* Cluster vs activity heatmap
* Interactive 3D PCA visualization using Plotly

All visualizations are available in:

```text
notebooks/dimensionality_reduction_clustering.ipynb
```

---

## Reproducibility

The project uses a Python virtual environment and a documented dependency file.

### Requirements

The main dependencies include:

```text
numpy
pandas
scikit-learn
matplotlib
seaborn
plotly
scipy
jupyter
notebook
```

### Environment Setup

Create the virtual environment:

```powershell
py -3.12 -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
pip install -r requirements.txt
```

### Run Jupyter Notebook

```powershell
jupyter notebook
```

Then open:

```text
notebooks/dimensionality_reduction_clustering.ipynb
```

### Reproducibility Configuration

The analysis uses fixed parameters and random seeds where applicable.

| Component              | Configuration    |
| ---------------------- | ---------------- |
| Standardization        | `StandardScaler` |
| PCA target             | ~95% variance    |
| PCA components         | 102              |
| K-Means                | `k=2`            |
| K-Means random state   | 42               |
| K-Means initialization | `n_init=10`      |
| DBSCAN                 | `eps=20`         |
| DBSCAN                 | `min_samples=5`  |
| Hierarchical           | `n_clusters=2`   |
| Hierarchical linkage   | Ward             |

---

## Test-Set Transformation

The test data was transformed using the same fitted preprocessing pipeline:

```text
Training Data
     │
     ├── Fit StandardScaler
     │
     ├── Fit PCA
     │
     └── Fit K-Means
     
Test Data
     │
     ├── Transform using trained StandardScaler
     │
     ├── Transform using trained PCA
     │
     └── Predict using trained K-Means
```

This ensures that the test data does not influence the fitted preprocessing or clustering model.

---

## Limitations

* Clustering was primarily evaluated on the training portion of the dataset.
* PCA retains approximately 95% of the original variance, so some information from the original 561-dimensional space is discarded.
* DBSCAN performance is sensitive to parameters such as `eps` and `min_samples`.
* The hierarchical dendrogram uses a representative sample of 300 observations because visualizing all observations would be difficult to interpret.
* The discovered clusters do not necessarily correspond exactly to all six predefined human activity classes.
* Known activity labels were used only for post-hoc interpretation and were not used during clustering.
* Internal clustering metrics measure mathematical cluster separation and do not necessarily indicate real-world semantic correctness.

---

## Project Structure

```text
Dimensionality-Reduction-Clustering/
│
├── data/
│   ├── raw/
│   │   └── UCI HAR Dataset/
│   ├── interim/
│   └── processed/
│
├── notebooks/
│   └── dimensionality_reduction_clustering.ipynb
│
├── reports/
│   └── final_results.md
│
├── src/
│
├── tests/
│
├── .gitignore
├── README.md
└── requirements.txt
```

> The raw, interim, and processed dataset files are excluded from Git using `.gitignore`.

---

## Key Findings

### PCA

The 561-dimensional feature space was reduced to **102 principal components**, retaining approximately **95% of the variance**.

### K-Means

The best K-Means configuration was:

```text
k = 2
Silhouette = 0.4154
```

### DBSCAN

The best evaluated DBSCAN configuration was:

```text
eps = 20
min_samples = 5
clusters = 2
noise = 159 observations
Silhouette = 0.4256
```

### Hierarchical Clustering

The selected hierarchical configuration was:

```text
n_clusters = 2
linkage = Ward
Silhouette = 0.4150
```

### Overall

DBSCAN achieved the highest internal Silhouette Score, while K-Means provided a particularly interpretable broad separation between stationary and movement-related activity patterns.

---

## Final Conclusion

This project demonstrates that **dimensionality reduction combined with unsupervised clustering can reveal meaningful structure in high-dimensional smartphone sensor data**.

PCA reduced the original 561-dimensional feature space to 102 components while preserving approximately 95% of the variance.

Among the evaluated configurations, DBSCAN achieved the highest Silhouette Score of **0.4256**, followed by K-Means at **0.4154** and Hierarchical Clustering at **0.4150**.

Post-hoc interpretation showed that the unsupervised models captured a meaningful broad distinction between stationary and movement-related activity patterns.

The results demonstrate the usefulness of combining PCA with multiple clustering techniques for exploratory analysis of high-dimensional sensor data.

---

## Internship Relevance

This project demonstrates practical understanding of:

* Unsupervised Machine Learning
* Dimensionality Reduction
* Principal Component Analysis
* Feature Standardization
* K-Means Clustering
* DBSCAN
* Hierarchical Clustering
* Elbow Method
* Silhouette Analysis
* Cluster Evaluation
* Data Visualization
* Reproducible Research
* Post-hoc Cluster Interpretation
* Python-based Data Science Workflows

---

## Dataset Citation

Reyes-Ortiz, J., Anguita, D., Ghio, A., Oneto, L., & Parra, X. (2013).

**Human Activity Recognition Using Smartphones [Dataset].**

UCI Machine Learning Repository.

DOI: `10.24432/C54S4K`

Dataset source:

https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones

---

## Author

**Deban Kumar Das D**

BCA — Data Science

GitHub: `Debankumardas`

---

## License

The dataset is provided by the UCI Machine Learning Repository under its applicable licensing terms.

This repository contains the analysis code, documentation, and project work built around the dataset.
