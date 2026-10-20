# Assignment 1 — Traveling Salesman Problem

Implementing and comparing exhaustive search, hill climbing and a genetic algorithm to find short tours through European cities.

Completed for **IN3050: Introduction to Artificial Intelligence and Machine Learning**, University of Oslo.

## Overview

The objective is to visit every selected city exactly once and return to the starting city while minimizing the total distance.

Tours are represented as permutations of city names. Distances are read from the supplied `european_cities.csv` file; geographical coordinates are used only for visualization.

The experiments explore the trade-off between exhaustive enumeration and stochastic optimization, using subsets of 6 and 10 cities and the full set of 24 cities.

## Implemented Methods

### Exhaustive search

Enumerates every permutation using `itertools.permutations`, calculates each complete tour's distance and retains the shortest.

This provides an exact reference for the smaller instances, but repeatedly evaluates equivalent tours with different starting positions.

### Hill climbing

Starts from a random tour and generates a candidate by swapping two adjacent cities. A candidate is accepted only if it shortens the tour.

The implementation stops at the first unsuccessful swap. It therefore does not examine the complete neighborhood before stopping and is not guaranteed to reach a local optimum.

Experiments use **20 runs** for both 10 and 24 cities.

### Genetic algorithm

Uses a population of city permutations and the following components:

- **Initialization:** randomly generated tours.
- **Parent selection:** weighted sampling favoring shorter tours.
- **Crossover:** a custom partially mapped crossover (PMX) implementation.
- **Mutation:** adjacent-city swaps, retaining both the original offspring and a mutated copy as candidates.
- **Survivor selection:** offspring can replace the current worst population member when they have a shorter tour.
- **Termination:** stops after five generations without improvement in the population's average distance, accumulated across the run.

Population sizes of **10, 50 and 100** are evaluated over **20 runs each**.

## Recorded Results

These results come from the saved assignment report and have not been independently reproduced for this repository.

### Exhaustive search

| Cities | Shortest tour distance | Recorded runtime |
| --- | ---: | ---: |
| 6 | 5,018.81 | Approximately 0.003 s |
| 10 | 7,486.31 | Approximately 19.46 s |

The recorded optimal 10-city tour is:

Copenhagen → Hamburg → Brussels → Dublin → Barcelona → Belgrade → Istanbul → Bucharest → Budapest → Berlin → Copenhagen.

### Hill climbing

Results across 20 runs:

| Cities | Best distance | Worst distance | Standard deviation |
| --- | ---: | ---: | ---: |
| 10 | 10,369.47 | 14,686.75 | 933.11 |
| 24 | 27,941.37 | 35,270.26 | 2,100.86 |

The recorded hill-climbing runs did not reach the exhaustive-search optimum for 10 cities. The early stopping rule limits the amount of local improvement performed.

### Genetic algorithm

The first recorded 24-city experiment produced:

| Population size | Best distance | Worst distance | Standard deviation |
| --- | ---: | ---: | ---: |
| 10 | 17,921.39 | 25,038.47 | 2,217.17 |
| 50 | 14,265.27 | 20,464.79 | 1,468.83 |
| 100 | 12,645.47 | 16,460.73 | 1,089.02 |

In this experiment, population size 100 achieved the shortest tour and the lowest variation across runs.

A separate recorded experiment also found the exhaustive-search optimum for 10 cities. Results vary between executions because the algorithms are stochastic.

## Visualizations

The notebook and PDF report include:

- Exhaustive-search tours for 6 and 10 cities.
- Example hill-climbing tours for 10 and 24 cities.
- A comparison of the genetic algorithm's best tour distance by generation for the three population sizes.
- The best 24-city genetic-algorithm tour from the first recorded experiment.

Lower tour distance indicates a better solution.

## Running the Notebook

Required tools:

- Python 3
- Jupyter Notebook or JupyterLab
- NumPy
- Matplotlib

The remaining imports use Python's standard library.

1. Open the assignment notebook.
2. Ensure `european_cities.csv` and `map.png` are available in the notebook's working directory.
3. Run the cells from top to bottom, or select **Run All**.

The exhaustive search for 10 cities is substantially slower than the smaller example. Do not attempt exhaustive enumeration of all 24 cities.

Exact outputs and timings will vary with random choices and the execution environment.

## Known Limitations and Reporting Corrections

This repository preserves the original coursework implementation and its saved outputs.

- **Reported means:** the original output divides the sum of 20 results by the number of cities rather than by 20. Those printed means are incorrect and are not reproduced in the tables above.
- **Runtime extrapolation:** the original 24-city exhaustive-search estimate is incorrect. For this implementation, a rough estimate should scale the 10-city runtime by the ratio of permutation counts, rather than their difference.
- **Randomness:** Python's `random` module is not consistently seeded, so the saved experiments are not exactly reproducible.
- **Convergence curves:** runs terminate at different generations. Later plotted averages include only runs still contributing data, rather than all 20 runs.
- **Selection loops:** the parent-weight calculation and offspring-replacement loop omit their final entries.
- **Evaluation counts:** the reported path counter tracks generated candidates, not every distance calculation or the number of unique tours inspected.

The results illustrate the behavior of this implementation, rather than a controlled benchmark of the algorithms in general.

## Attribution and Scope

The assignment supplied the problem description, distance dataset, map and plotting helper code.

My work comprises the search algorithms, supporting functions, experiment code and analysis presented in the submission.

The optional IN4050 hybrid-algorithm extension was not implemented.
