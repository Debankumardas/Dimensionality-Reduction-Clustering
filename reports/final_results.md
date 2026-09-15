# Final Results Report

## 1. Project Overview

This project investigates whether dimensionality reduction and unsupervised clustering can reveal meaningful activity patterns in high-dimensional smartphone sensor data.

The analysis uses the **UCI Human Activity Recognition Using Smartphones** dataset, which contains 10,299 observations and 561 numerical sensor-derived features representing six human activities.

### Research Question

> Can PCA and unsupervised clustering reveal meaningful activity patterns in high-dimensional smartphone sensor data?

---

## 2. Methodology

The analysis followed the following pipeline:

1. Loaded the UCI Human Activity Recognition Using Smartphones dataset.
2. Combined the training and testing feature structures while preserving the original train/test separation for evaluation.
3. Validated the dataset dimensions, feature names, and missing values.
4. Resolved duplicate feature names while retaining all 561 original features.
5. Standardized the numerical features using `StandardScaler`.
6. Applied Principal Component Analysis (PCA).
7. Selected the number of principal components required to retain approximately 95% of the variance.
8. Evaluated K-Means clustering using the Elbow Method and Silhouette Score.
9. Evaluated DBSCAN across multiple `eps` values.
10. Applied Agglomerative Hierarchical Clustering using Ward linkage.
11. Compared the clustering methods using internal validation metrics.
12. Visualized clusters using 2D PCA projections, a dendrogram, and an interactive 3D PCA visualization.
13. Used the known activity labels only for post-hoc interpretation.

---

## 3. PCA Results

The original dataset contained:

- **561 features**
- **7,352 training observations**
- **2,947 test observations**

PCA reduced the training data from 561 dimensions to **102 principal components**, while retaining approximately **95% of the total variance**.

This substantially reduced the dimensionality while preserving most of the information contained in the original feature space.

---

## 4. K-Means Results

K-Means clustering was evaluated for values of `k` from 2 to 10.

The Elbow Method was used to examine the reduction in inertia as the number of clusters increased.

The Silhouette Score identified:

- **Optimal k = 2**
- **Silhouette Score = 0.4154**

The two-cluster solution provided a meaningful broad separation between stationary and movement-related activity patterns.

---

## 5. DBSCAN Results

DBSCAN was evaluated using multiple `eps` values.

The selected configuration was:

- **eps = 20**
- **min_samples = 5**
- **Number of clusters = 2**
- **Noise observations = 159**
- **Noise percentage = 2.16%**
- **Silhouette Score = 0.4256**

DBSCAN achieved the highest Silhouette Score among the evaluated clustering configurations.

Only a small proportion of observations were classified as noise.

---

## 6. Hierarchical Clustering Results

Agglomerative Hierarchical Clustering was performed using:

- **Number of clusters = 2**
- **Linkage = Ward**

The resulting Silhouette Score was:

- **0.4150**

A dendrogram was also generated using a representative sample of 300 observations to make the hierarchical structure easier to visualize.

---

## 7. Clustering Comparison

| Method | Configuration | Clusters | Noise | Silhouette |
|---|---|---:|---:|---:|
| K-Means | k=2 | 2 | 0 | 0.4154 |
| DBSCAN | eps=20, min_samples=5 | 2 | 159 | **0.4256** |
| Hierarchical | 2 clusters, Ward | 2 | 0 | 0.4150 |

Based on the Silhouette Score, **DBSCAN provided the strongest internal clustering result** among the evaluated methods.

However, K-Means produced a particularly interpretable broad separation between stationary and movement-related observations.

---

## 8. Post-Hoc Activity Interpretation

The known activity labels were **not provided to any clustering algorithm**.

They were introduced only after clustering to interpret the discovered structure.

The K-Means results showed a strong broad distinction between:

- Stationary activities: `LAYING`, `SITTING`, and `STANDING`
- Movement-related activities: `WALKING`, `WALKING_UPSTAIRS`, and `WALKING_DOWNSTAIRS`

This indicates that the unsupervised algorithms were able to discover meaningful structure without using the known activity labels during model fitting.

The clusters should therefore be interpreted as **discovered activity patterns**, rather than exact replacements for the six predefined activity classes.

---

## 9. Visualization Results

The project includes:

- PCA explained variance analysis
- PCA scree plot
- K-Means Elbow plot
- K-Means Silhouette analysis
- 2D PCA cluster visualizations
- DBSCAN noise visualization
- Hierarchical clustering dendrogram
- Interactive 3D PCA visualization
- Cluster-size comparison
- Cluster-versus-activity heatmap

These visualizations provide both quantitative and qualitative evidence for the discovered clustering structure.

---

## 10. Reproducibility

The analysis uses fixed configurations and random seeds where applicable.

### Main configuration

- Standardization: `StandardScaler`
- PCA target: approximately 95% explained variance
- PCA components used for clustering: `102`
- K-Means: `k=2`, `random_state=42`, `n_init=10`
- DBSCAN: `eps=20`, `min_samples=5`
- Hierarchical clustering: `n_clusters=2`, `linkage="ward"`

The project dependencies are documented in `requirements.txt`.

---

## 11. Limitations

- Clustering was primarily evaluated on the training portion of the dataset.
- PCA retains approximately 95% of the original variance, meaning some information is discarded.
- DBSCAN is sensitive to parameters such as `eps` and `min_samples`.
- The hierarchical dendrogram uses a sample of 300 observations because visualizing all observations would be difficult to interpret.
- The discovered clusters do not necessarily correspond exactly to all six predefined activity classes.
- The known activity labels were used only for post-hoc interpretation and not during clustering.

---

## 12. Final Conclusion

The analysis demonstrates that PCA combined with unsupervised clustering can reveal meaningful structure in high-dimensional smartphone sensor data.

PCA successfully reduced the original 561-dimensional feature space to 102 components while retaining approximately 95% of the variance.

Among the evaluated clustering configurations, DBSCAN achieved the highest Silhouette Score of **0.4256**, while K-Means achieved **0.4154** and Hierarchical Clustering achieved **0.4150**.

The post-hoc interpretation further showed that the discovered clusters captured a meaningful broad distinction between stationary and movement-related activity patterns.

Overall, the results support the use of dimensionality reduction and unsupervised clustering as effective exploratory techniques for high-dimensional sensor data.

---

## Dataset

**UCI Human Activity Recognition Using Smartphones**

Reyes-Ortiz, J., Anguita, D., Ghio, A., Oneto, L., & Parra, X. (2013).

UCI Machine Learning Repository.

DOI: `10.24432/C54S4K`