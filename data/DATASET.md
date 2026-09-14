# Dataset Documentation

## Dataset

**Human Activity Recognition Using Smartphones**

## Source

UCI Machine Learning Repository

Dataset ID: 240

Official Dataset Page:
https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones

DOI:
https://doi.org/10.24432/C54S4K

## Dataset Description

The Human Activity Recognition Using Smartphones dataset contains sensor measurements collected from 30 volunteers performing activities of daily living while carrying a smartphone equipped with an accelerometer and gyroscope.

The smartphone was worn around the waist and sensor signals were recorded at a constant frequency of 50 Hz.

The signals were processed into fixed-width sliding windows, and numerical features were extracted from both the time and frequency domains.

## Dataset Size

- Instances: 10,299
- Numerical features: 561
- Subjects: 30
- Activities: 6
- Missing values: None

## Activities

The dataset contains six activity classes:

1. WALKING
2. WALKING_UPSTAIRS
3. WALKING_DOWNSTAIRS
4. SITTING
5. STANDING
6. LAYING

## Features

The dataset contains 561 numerical features derived from smartphone sensor signals.

These features include measurements derived from:

- Triaxial accelerometer signals
- Body acceleration
- Gravity acceleration
- Gyroscope signals
- Time-domain measurements
- Frequency-domain measurements

## Dataset Usage in This Project

The 561 numerical features will be used as the input space for dimensionality reduction and unsupervised clustering.

The activity labels will **not** be used as input features for clustering.

The analysis will follow this process:

1. Load the numerical feature matrix.
2. Perform data quality checks.
3. Standardize the numerical features.
4. Apply Principal Component Analysis (PCA).
5. Analyze explained variance.
6. Apply K-Means clustering.
7. Apply DBSCAN.
8. Apply Hierarchical Clustering.
9. Compare clustering results.
10. Use the original activity labels only for post-hoc interpretation where appropriate.

This prevents the clustering algorithms from receiving the known activity classes during model fitting.

## Why This Dataset Was Selected

This dataset is suitable for the project because it contains 561 numerical features for 10,299 observations.

The high-dimensional feature space makes PCA meaningful for dimensionality reduction and visualization.

The dataset is also suitable for evaluating multiple unsupervised clustering algorithms because its observations represent different human activities recorded from smartphone sensor measurements.

## License

The dataset is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0) license.

Appropriate attribution will be provided when the dataset is used or redistributed.

## Citation

Reyes-Ortiz, J., Anguita, D., Ghio, A., Oneto, L., & Parra, X. (2013).

**Human Activity Recognition Using Smartphones [Dataset].**

UCI Machine Learning Repository.

https://doi.org/10.24432/C54S4K

## Important Note

The raw dataset will not be committed to this Git repository.

The repository will contain the code, notebooks, documentation, and reproducible analysis workflow required to obtain and process the dataset.