# Assignment: Meta-heuristic Optimization for Parameter Estimation

## Overview

This assignment focuses on applying three meta-heuristic optimization algorithms—Particle Swarm Optimization (PSO), Genetic Algorithm (GA), and Simulated Annealing (SA)—to estimate the parameters of a logistic regression model. The goal is to minimize the negative log-likelihood, incorporating L1 or L2 regularization, using the Breast Cancer Wisconsin (Diagnostic) dataset.

---

## Dataset

**Dataset Source:** UCI Machine Learning Repository  
- **Input Features:** Characteristics of cell nuclei (e.g., radius, texture).  
- **Binary Label:** Malignant (M) or Benign (B).  
- **Objective:** Train a logistic regression classifier to distinguish between malignant and benign tumors.

---

## Part A: Conceptual Questions

### A.1 High-level Algorithm Descriptions
1. **PSO:** Navigates the parameter space by simulating a swarm of particles, where each particle adjusts its position based on personal experience and the swarm's best-known position.
2. **GA:** Generates new solutions through selection, crossover, and mutation, ensuring diversity in the population.
3. **SA:** Accepts worse solutions probabilistically to avoid local minima, using a cooling schedule to reduce acceptance probability over time.

### A.2 Exploration vs. Exploitation
1. **Controlling Factors:**  
   - PSO: Inertia weight, cognitive, and social constants.  
   - GA: Mutation rate and crossover rate.  
   - SA: Initial temperature and cooling rate.
2. **Examples:** Increasing mutation rate in GA enhances exploration, while reducing inertia weight in PSO promotes exploitation.

### A.3 Convergence and Local Minima
1. **Escape Mechanisms:**  
   - PSO: Swarm diversity.  
   - GA: Genetic diversity through mutation and crossover.  
   - SA: Acceptance of worse solutions.
2. **Convergence Speed:** PSO typically converges faster but risks premature convergence; GA balances exploration/exploitation; SA avoids local minima at the cost of slower convergence.

### A.4 Regularization Insights
1. **L1 vs L2 Regularization:**  
   - L1 promotes sparsity by shrinking coefficients to zero.  
   - L2 reduces magnitude but retains all coefficients.
2. **Impact on Solutions:** L1 simplifies models by selecting fewer features; L2 ensures smoother weight distribution.

---

## Part B: Mathematical Formulation

### B.1 Negative Log-Likelihood (NLL) Derivation
The NLL for logistic regression is:
\[
\mathcal{L}\left(\beta_{0}, \beta\right) = -\sum_{i=1}^{N} \left[y_i \ln(p_i) + (1-y_i) \ln(1-p_i)\right]
\]
where \( p_i = \sigma(\beta_0 + \beta^\top x_i) \).

### B.2 Gradient Derivations
The gradient of \( \mathcal{L} \) with respect to \( (\beta_0, \beta) \) is:
\[
\frac{\partial \mathcal{L}}{\partial \beta_0} = \sum_{i=1}^{N} (p_i - y_i)
\]
\[
\frac{\partial \mathcal{L}}{\partial \beta} = \sum_{i=1}^{N} (p_i - y_i)x_i
\]

### B.3 Regularization Terms
1. **L2 Penalty:** \( \lambda \|\beta\|_2^2 \).  
2. **L1 Penalty:** \( \lambda \|\beta\|_1 \).  

Incorporating these penalties alters the objective function’s shape, encouraging sparsity for L1 or smoothness for L2 regularization.

---

## Part C: Implementation & Experiments

### C.1 Data Preprocessing
- Convert labels M/B to binary 0/1.
- Handle missing values via imputation or removal.
- Normalize features for consistent scaling.
- Split data into 70% training and 30% test sets.

### C.2 Algorithm Implementations
1. **PSO:** Define particles representing \( (\beta_0, \beta_1, ..., \beta_d) \), with inertia weight and cognitive/social constants tuned for convergence.
2. **GA:** Use chromosomes for solutions, implementing selection, crossover, and mutation with controlled rates.
3. **SA:** Start with a high temperature and gradually cool using a predefined schedule.

### C.3 Objective Function and Regularization
Objective function:
\[
\mathcal{L}_{\text{reg}} = \mathcal{L}\left(\beta_0, \beta\right) + \lambda R(\beta)
\]
where \( R(\beta) \) is either L1 or L2 penalty.

### C.4 Hyperparameter Tuning
- PSO: Tune inertia weight and social constants.
- GA: Adjust mutation/crossover rates.
- SA: Optimize initial temperature and cooling schedule.

### C.5 Performance Metrics
- Training loss vs iterations.
- Test set metrics: accuracy, precision, recall, F1-score, AUC.
- Convergence plots for each algorithm.

---

## Part D: Analysis and Discussion

### D.1 Convergence Characteristics
Analyze speed of convergence and identify signs of premature convergence for each algorithm.

### D.2 Hyperparameter Sensitivity
Evaluate the impact of key hyperparameters on performance metrics and optimization behavior.

### D.3 Model Interpretability
Report final weights \( (\beta_0, ..., \beta_d) \), highlighting important features influenced by regularization type.

### D.4 Recommendations
Provide practical advice on selecting algorithms based on computational constraints or feature space dimensionality.

---

## Deliverables

**Written Report (3–5 pages):**
- Conceptual answers (Part A).
- Mathematical derivations (Part B).
- Implementation details and results analysis (Part C).

**Code Submission:**
Include well-documented scripts/notebooks with a README for reproducibility.

**Plots & Tables:**
Convergence curves, performance metrics tables, and additional visualizations.

---

## Grading Breakdown

| Component                  | Weight |
|----------------------------|--------|
| Conceptual Understanding   | 20%    |
| Mathematical Rigor         | 20%    |
| Implementation & Results   | 40%    |
| Analysis & Discussion      | 20%    |

---

## Policies & Tips

- Collaboration allowed for idea exchange; code/write-ups must be individual.
- Test algorithms on smaller datasets before scaling up.
- Demonstrate experiments with both L1 and L2 regularization.
