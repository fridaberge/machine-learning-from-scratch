# Machine Learning from Scratch

Python and NumPy implementations exploring evolutionary optimization, supervised learning and dimensionality reduction.

Developed for **IN3050: Introduction to Artificial Intelligence and Machine Learning** at the **University of Oslo**, spring 2025.

## Overview

This repository contains three coursework assignments, progressing from search and optimization to classification and unsupervised learning.

The emphasis is on understanding algorithms through explicit implementations, experiments and visualizations—not just calling model-training APIs.

**NumPy** is used for numerical computations and **Matplotlib** for visualization. **Scikit-learn** is used for dataset generation in Assignment 2, and for clustering and evaluation models in Assignment 3.

## Assignments

| Assignment | Topic | Methods and experiments |
| --- | --- | --- |
| [Assignment 1](./Assignment1/) | Traveling Salesman Problem | Exhaustive search, hill climbing and a genetic algorithm |
| [Assignment 2](./Assignment2/) | Supervised learning | Linear and logistic regression, one-vs-rest classification and a multilayer perceptron |
| [Assignment 3](./Assignment3/) | Unsupervised learning | PCA implementation, image reconstruction and K-means clustering |

### 1. Traveling Salesman Problem

Find short round-trip tours through European cities and compare exact search with stochastic optimization.

- Permutation-based tour representation.
- Exhaustive search on smaller city subsets.
- Hill climbing with adjacent-city swaps.
- Genetic algorithm with crossover, mutation and survivor selection.
- Comparisons across population sizes and repeated runs.

### 2. Supervised Learning

Explore gradient-based classification on a synthetic two-feature dataset.

- Binary classification with linear and logistic regression.
- Multiclass classification using one-vs-rest logistic regression.
- A single-hidden-layer neural network.
- Feature-scaling and hyperparameter experiments.
- Loss curves, decision regions and held-out evaluation.

### 3. Unsupervised Learning

Implement PCA step by step and investigate its applications.

- Centering, covariance computation and eigendecomposition.
- Low-dimensional visualization of synthetic and Iris data.
- Face-image reconstruction with different component counts.
- K-means clustering using scikit-learn.
- Evaluation of cluster representations through logistic regression.

## Getting Started

### Requirements

- Python 3
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook or JupyterLab

Install the dependencies:

```bash
python -m pip install numpy matplotlib scikit-learn jupyterlab
```

Open a notebook in **VS Code** or **JupyterLab**, using its assignment folder as the working directory, and run the cells from top to bottom.

Keep supporting datasets, images and reference files in their assignment folders. The face-image dataset in Assignment 3 may require an initial download.

See each assignment's README for specific instructions and recorded results.

## Results and Limitations

The notebooks and PDF reports preserve the original coursework experiments and outputs.

These are educational implementations, not production-ready models or controlled benchmarks. Some reporting and implementation issues remain in the original submissions; the assignment READMEs document them so the results can be interpreted appropriately.

Randomized experiments may produce different results when rerun.

## Attribution

**Author:** Frida Berge

The coursework builds on assignment templates, datasets, helper functions and starter code supplied by the course. Individual READMEs distinguish these materials from my contributions and document acknowledged assistance.
