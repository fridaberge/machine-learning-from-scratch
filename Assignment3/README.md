# Assignment 3 — Unsupervised Learning

Implementing Principal Component Analysis (PCA) with NumPy and exploring K-means clustering through visualization and downstream classification.

Completed for **IN3050: Introduction to Artificial Intelligence and Machine Learning**, University of Oslo.

## Overview

This assignment explores two uses of unsupervised learning:

- **Dimensionality reduction:** implementing PCA and applying it to visualization and image reconstruction.
- **Clustering:** applying scikit-learn's K-means and evaluating how well cluster membership represents known classes.

PCA is implemented using NumPy operations. K-means and the logistic regression models used for evaluation come from scikit-learn.

## Files

| File | Description |
| --- | --- |
| `IN3050_assignment_3.ipynb` | Notebook containing implementations, experiments, plots and comments |
| `IN3050_assignment_3.pdf` | Exported report with saved outputs |
| `data_assignment3.py` | Supplied dataset-loading utilities |
| `PCAanswer1.pkl` | Supplied reference output for PCA testing |
| `PCAanswer2.pkl` | Supplied reference output for PCA testing |

## PCA Implementation

The implementation follows these steps:

1. Center each feature by subtracting its mean.
2. Compute the sample covariance matrix.
3. Calculate eigenvalues and eigenvectors with `np.linalg.eig`.
4. Sort the eigenpairs by descending eigenvalue.
5. Project the centered data onto the selected principal components.

The notebook includes assertion-based checks for centering, covariance computation, eigenpair sorting and the final PCA projection.

### Synthetic data

Experiments visualize:

- Original and centered data.
- Principal-component directions.
- Projection from two dimensions to one.
- How dimensionality reduction affects class separation under two different labelings.

These examples investigate why retaining high variance does not necessarily preserve the information needed for classification.

### Iris visualization

The four-feature Iris dataset is projected onto two principal components and compared with a visualization using two selected original features.

### Face-image reconstruction

PCA is used to reduce the dimensionality of face images and reconstruct them by projecting back into the original feature space and restoring the feature means.

Reconstructions are explored with **20, 100, 200, 500 and 1,000 components**. The saved visual comparisons show more image detail retained as the number of components increases.

These experiments demonstrate lossy reconstruction rather than measuring compressed file sizes.

## K-Means Clustering

K-means is applied to the two-dimensional PCA representation of Iris using **2, 3, 4 and 5 clusters**.

The notebook compares cluster assignments with the true species labels and plots the learned cluster centers.

### Quantitative evaluation

Cluster assignments are one-hot encoded and used as inputs to logistic regression, with the true Iris species as targets.

A separate logistic regression model trained directly on the two PCA coordinates provides a comparison.

| Logistic regression input | Recorded training accuracy |
| --- | ---: |
| Two PCA coordinates | 96.67% |
| Cluster membership: 2 clusters | 66.67% |
| Cluster membership: 3 clusters | 88.67% |
| Cluster membership: 4 clusters | 88.00% |
| Cluster membership: 5 clusters | 90.00% |

These are saved submission results, not independently reproduced benchmarks.

The PCA-coordinate baseline achieved the highest training accuracy. Cluster-based accuracy generally increased with more clusters, but not monotonically.

**All models are evaluated on their training data.** These scores measure model fit, not generalization to unseen samples.

## Running the Notebook

Install the dependencies:

```bash
python -m pip install numpy matplotlib scikit-learn jupyterlab
```

Open `IN3050_assignment_3.ipynb` in VS Code or JupyterLab and run the cells from top to bottom.

Keep `data_assignment3.py` and both reference `.pkl` files in the notebook's working directory.

The face dataset may require an internet connection for its initial download. Its covariance-matrix eigendecomposition is also more computationally demanding than the smaller examples.

## Known Limitations

- **Repeated eigenvalues:** eigenpair sorting uses value lookup, which can select the same eigenvector repeatedly when eigenvalues are equal.
- **Eigenvector visualization:** the first-component plotting cell selects a row of the eigenvector matrix rather than its first column.
- **Random feature selection:** the Iris feature-selection code does not sample all four features as intended.
- **Reproducibility:** K-means initialization and random feature selection are not fixed with consistent seeds.
- **Evaluation scope:** no held-out evaluation or quantitative image-reconstruction metric is included.
- **Optional extension:** variance-threshold-based component selection remains an unimplemented IN4050 exercise.

## Attribution

The assignment supplied the notebook structure, dataset utilities and reference tests. My contributions include the completed PCA functions, image reconstruction, experiments, visualizations and analysis.

The notebook acknowledges assistance from UiO GPT for descending-sort syntax and ChatGPT for one-hot encoding.
