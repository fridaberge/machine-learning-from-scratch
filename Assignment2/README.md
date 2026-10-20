# Assignment 2 — Supervised Learning with NumPy

Exploring gradient-based learning through binary and multiclass classification, comparing linear models with a multilayer perceptron.

Completed for **IN3050: Introduction to Artificial Intelligence and Machine Learning**, University of Oslo.

## Overview

This assignment investigates how model architecture, learning rate, feature scaling and stopping criteria affect classification performance.

The classifiers use explicit NumPy operations rather than machine-learning training APIs. Scikit-learn is used only to generate the synthetic dataset.

## Dataset

The supplied dataset-generation code creates **5,000 samples**, each with two numerical features, distributed across ten classes.

Two classification tasks use the same features:

- **Binary classification:** original labels 0–5 become class 0; labels 6–9 become class 1.
- **Multiclass classification:** retain the original ten classes.

The data is shuffled and split into:

| Split | Samples | Proportion |
| --- | ---: | ---: |
| Training | 3,000 | 60% |
| Validation | 1,000 | 20% |
| Test | 1,000 | 20% |

Dataset generation and shuffling use the fixed seed `424242`.

## Implemented Methods

### Linear regression classifier

Uses gradient descent to fit a linear model, then applies a threshold to produce binary predictions.

Experiments explore learning rates and epoch counts through randomized hyperparameter search. A custom standardization function is also implemented.

### Logistic regression

Implements sigmoid-based binary classification with:

- Probability predictions.
- Binary cross-entropy loss tracking.
- Training and validation accuracy histories.
- Tolerance-based early stopping.
- Learning-rate and tolerance tuning.

### One-vs-rest multiclass classification

Trains one logistic regression model for each of the ten classes. Predictions select the class whose model produces the highest probability score.

Experiments include hyperparameter tuning, decision-region plots and comparisons of average classifier scores between training and validation data.

### Multilayer perceptron

Extends the supplied single-hidden-layer network with:

- A completed forward pass.
- Sigmoid hidden-layer activations and a linear output.
- Backpropagation.
- Loss and accuracy histories.
- Tolerance-based early stopping.
- Experiments with learning rate, tolerance and hidden-layer size.
- Repeated training runs to investigate variability.

## Recorded Results

These values are taken from the saved submission outputs and have not been independently reproduced.

### Hyperparameter-search results

| Model | Best reported validation accuracy | Reported settings |
| --- | ---: | --- |
| Linear regression, initial tuning | 77.5% | Learning rate 0.0276; 94 epochs |
| Logistic regression | 77.3% | Learning rate 0.0699; tolerance 0.0452; 3 epochs |
| One-vs-rest logistic regression | 50.4% | Learning rate 0.4; reported tolerance 0.006 |
| MLP | 85.0% | Learning rate 0.0002; tolerance 0.00002; 10 hidden units; 729 epochs |

These are search-stage results, not the final held-out test scores. The tuning routines record the best metrics but do not restore the corresponding model weights.

### Final binary evaluation

| Model | Training accuracy | Validation accuracy | Test accuracy |
| --- | ---: | ---: | ---: |
| Linear regression | 77.6% | 77.4% | 76.7% |
| Logistic regression | 76.3% | 77.3% | 76.5% |
| MLP | 69.7% | 68.0% | 68.7% |

The two linear models achieved similar test accuracy in the recorded evaluation.

Although the MLP reached a higher validation accuracy during tuning, its final evaluated state performed considerably worse. The notebook retrains the MLP after tuning and does not preserve the best model checkpoint, so the final row does not evaluate the model that achieved 85.0%.

## Visualizations

The notebook and exported report contain:

- Binary and ten-class dataset plots.
- Linear and nonlinear decision regions.
- Training and validation loss curves.
- Training and validation accuracy curves.

These figures document the saved experiments; they should be interpreted alongside the implementation limitations below.

## Running the Notebook

### Requirements

- Python 3
- Jupyter Notebook or JupyterLab
- NumPy
- Matplotlib
- Scikit-learn, for dataset generation only

Install the dependencies:

```bash
python -m pip install numpy matplotlib scikit-learn jupyterlab
```

Open the assignment notebook in VS Code or JupyterLab, then run its cells from top to bottom.

The dataset is generated within the notebook, so no external dataset download is required. Training times and stochastic results may vary between executions.

## Known Limitations

This repository preserves the original coursework implementation and recorded outputs.

- **Scaling experiments:** some scaler outputs are discarded, while tuning and reporting helpers use the original data. The saved results therefore do not establish a reliable scaled-versus-unscaled comparison.
- **Best-model preservation:** tuning stores metrics and settings, but not the corresponding weights. Later plots and evaluations may use a different model state.
- **Tolerance reporting:** parts of the multiclass and MLP tuning code record `tols[i]` rather than the tolerance indexed by the inner loop, so reported settings may not match the selected run.
- **MLP objective consistency:** backpropagation uses linear-output residuals, while the monitored loss uses sigmoid-transformed outputs and binary cross-entropy. The training updates and monitored objective are not aligned.
- **Stopping safeguards:** the logistic regression and MLP training loops rely on tolerance-based stopping rather than enforcing the supplied epoch limit.
- **Per-class analysis:** average probability scores are reported, but these are not per-class accuracy, precision or recall.
- **Final multiclass evaluation:** the original final table compares multiclass predictions against binary targets. Those scores are invalid and are omitted here.
- **Precision and recall:** the requested binary class-1 precision and recall are not correctly reported in the submission.
- **Reproducibility:** randomized tuning and network initialization are not consistently seeded.

## Attribution and Scope

The assignment supplied the dataset-generation code, plotting utilities, linear regression classifier and an incomplete MLP implementation. Course exercise code was also permitted.

My submission builds on these materials through classifier implementations and extensions, tuning routines, scaling functions, experiment code and recorded evaluations.

The optional IN4050 softmax classifier and multiclass neural-network extensions are not included.
