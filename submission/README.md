# Meta-heuristic Optimization for Parameter Estimation

This repository contains the submission materials for the assignment on applying meta-heuristic optimization algorithms (PSO, GA, and SA) to parameter estimation in logistic regression models with L1/L2 regularization.

## Repository Structure

```
submission/
├── Part_A/                # Conceptual questions
│   ├── A1.md             # High-level algorithm descriptions
│   ├── A2.md             # Exploration vs. exploitation
│   ├── A3.md             # Convergence and local minima
│   └── A4.md             # Regularization insights
├── Part_B/                # Mathematical formulations
│   └── Ans_B.pdf         # Handwritten mathematical derivations
├── Part_C/                # Implementation
│   └── solution.ipynb    # Code implementation of meta-heuristic methods
├── Part_D/                # Analysis and discussion
│   └── Analysis.md       # Findings and analysis of implementation results
└── ODSM_Assignment_Report.pdf  # Comprehensive report of the entire assignment
```

## Contents Description

### Part A: Conceptual Questions
Contains markdown files addressing fundamental concepts of meta-heuristic optimization algorithms:
- [A1.md](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_A/A1.md): Describes how PSO navigates parameter space, how GA generates solutions to maintain diversity, and how SA accepts worse solutions to avoid local minima.
- [A2.md](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_A/A2.md): Discusses controlling factors for exploration/exploitation balance in each algorithm.
- [A3.md](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_A/A3.md): Examines escape mechanisms and convergence characteristics.
- [A4.md](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_A/A4.md): Explains differences between L1 and L2 regularization from an optimization perspective.

### Part B: Mathematical Formulation
- [Ans_B.pdf](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_B/Ans_B.pdf): Contains handwritten derivations of:
  - B.1: Negative Log-Likelihood (NLL) for logistic regression
  - B.2: Gradient derivations for the NLL function
  - B.3: L1 and L2 regularization terms and their effects

### Part C: Implementation & Experiments
- [solution.ipynb](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_C/solution.ipynb): Jupyter notebook containing:
  - Data preprocessing for the Breast Cancer Wisconsin dataset
  - Implementation of PSO, GA, and SA algorithms
  - Integration of L1 and L2 regularization
  - Performance comparison across algorithms and regularization types
  - Hyperparameter tuning experiments

### Part D: Analysis and Discussion
- [Analysis.md](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/Part_D/Analysis.md): Comprehensive analysis including:
  - Convergence characteristics comparison
  - Hyperparameter sensitivity analysis
  - Model interpretability and feature importance
  - Practical recommendations for algorithm selection

### Comprehensive Report
- [ODSM_Assignment_Report.pdf](https://github.com/VedantJoshi-2024/ODSM_Assignment_2/tree/main/submission/ODSM_Assignment_Report.pdf): Complete report integrating all components:
  - Conceptual foundations
  - Mathematical derivations
  - Implementation details
  - Results and analysis
  - Conclusions and recommendations

## How to Navigate

1. Start with the comprehensive report for an overview of the entire project
2. Explore Part_A for conceptual understanding
3. Review Part_B for mathematical foundations
4. Examine Part_C for implementation details
5. Study Part_D for results analysis and insights

## Technologies Used

- Python for implementation
- Jupyter Notebook for interactive code and visualization
- Meta-heuristic algorithms: PSO, GA, and SA
- Logistic regression with L1/L2 regularization
