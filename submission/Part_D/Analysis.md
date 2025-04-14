# Part D: Analysis and Discussion

## D.1 Convergence Characteristics

### Compare how quickly each algorithm finds a near-optimal solution

Based on the experimental results, the three meta-heuristic algorithms exhibit distinct convergence patterns in optimizing logistic regression parameters:

- **Particle Swarm Optimization (PSO)**: Demonstrates steady and consistent convergence throughout iterations. The cost function value decreases smoothly, indicating a balanced exploration-exploitation strategy. PSO reaches a satisfactory solution within approximately 75 iterations with minimal fluctuation.
- **Genetic Algorithm (GA)**: Shows rapid initial convergence in the first 20-30 generations, followed by a slower rate of improvement. This suggests that GA quickly identifies promising regions of the solution space but requires more generations to fine-tune the solution. Despite this, GA achieved the highest test accuracy at 98.83%.
- **Simulated Annealing (SA)**: Exhibits a more gradual convergence pattern compared to PSO and GA. The initial high-temperature phase allows for extensive exploration, resulting in occasional cost increases, but the overall trend shows steady improvement as the temperature decreases.

When comparing raw convergence speed, GA appears to reach lower cost values faster than the other algorithms for this specific problem, though all three eventually reach comparable final performance.

### Discuss any signs of premature convergence

Examining the convergence plots reveals important insights regarding potential premature convergence:

- **PSO**: Shows no clear signs of premature convergence as the cost function continues to decrease gradually throughout the iterations. The consistent improvement suggests PSO maintains sufficient diversity in the particle swarm, avoiding local optima traps.
- **GA**: There are slight plateaus in the cost function after approximately 50 generations in some runs, which could indicate potential premature convergence. This might be attributed to the population losing genetic diversity, causing the algorithm to get stuck in a local optimum. However, varying mutation rates (particularly higher rates) helps mitigate this issue.
- **SA**: The cooling schedule significantly impacts convergence behavior. With a cooling rate of 0.95, SA showed a balanced approach without clear signs of premature convergence. However, with faster cooling rates (0.8), there were indications of potential premature convergence as the algorithm quickly lost its ability to escape local optima.

None of the algorithms showed severe premature convergence issues, suggesting appropriate parameter settings were used. The balance between exploration and exploitation appears well-maintained across all three approaches.

## D.2 Hyperparameter Sensitivity

### Show and interpret the effect of varying key hyperparameters

The experimental results demonstrate significant impacts of key hyperparameters on algorithm performance:

- **PSO - Inertia Weight (w)**:
    - Low inertia weight (w=0.4): Results in faster initial convergence but higher risk of getting trapped in local optima
    - Medium inertia weight (w=0.7): Provides balanced exploration-exploitation, leading to the best overall performance
    - High inertia weight (w=0.9): Causes slower convergence due to excessive exploration, but potentially better global search capability

The experiments show that w=0.7 produces the most consistent convergence pattern, balancing the particle's tendency to continue in its current direction with the pull toward personal and global best positions.

- **GA - Mutation Rate**:
    - Low mutation rate (0.05): Leads to faster initial convergence but limited exploration capability
    - Medium mutation rate (0.1): Provides a good balance, allowing sufficient exploration while maintaining convergence speed
    - High mutation rate (0.2): Increases exploration but slows convergence and introduces more variability in performance

The optimal mutation rate of approximately 0.1 maintains sufficient genetic diversity without excessively disrupting good solutions, yielding the highest classification accuracy (98.83% on test data).

- **SA - Cooling Rate**:
    - Fast cooling (0.8): Results in rapid initial progress but increased risk of premature convergence
    - Medium cooling (0.9): Balances exploration and exploitation phases
    - Slow cooling (0.95): Allows for more thorough exploration of the solution space, potentially finding better solutions at the cost of slower convergence

The experiments indicate that a cooling rate of 0.95 produces the most reliable results for this problem, allowing SA sufficient time to explore before settling into exploitation.

### Indicate which hyperparameters are most critical to each algorithm's success

Based on the experimental results, the most critical hyperparameters for each algorithm are:

- **PSO**: Inertia weight (w) is the most critical parameter as it directly controls the balance between global and local exploration. The experimental results show that changing w from 0.4 to 0.9 significantly impacts convergence behavior and final solution quality. The cognitive and social constants (c1, c2) also affect performance but to a lesser extent than the inertia weight.
- **GA**: Mutation rate emerges as the most critical parameter for GA performance. It directly affects the algorithm's ability to maintain diversity and escape local optima. The experimental results demonstrate that varying mutation rate from 0.05 to 0.2 substantially alters convergence patterns. Crossover rate also impacts performance but shows less dramatic effects in the experiments.
- **SA**: Cooling rate is undoubtedly the most critical parameter for SA, as it determines how quickly the algorithm transitions from exploration to exploitation. The experiments with cooling rates ranging from 0.8 to 0.95 reveal significant differences in convergence behavior and final solution quality. Initial temperature is also important but primarily affects the early phases of the algorithm.

The sensitivity analysis confirms that properly tuning these critical hyperparameters is essential for achieving optimal performance in logistic regression optimization.

## D.3 Model Interpretability

### Report the final logistic regression weights (including β₀)

The final logistic regression weights (coefficients) varied across the different optimization algorithms and regularization methods. While the exact numerical values for all 31 features (30 features plus β₀) are not presented here for brevity, key observations include:

- **PSO with L2 regularization**:
    - Produced weights that achieved 97.66% test accuracy
    - Weight distribution showed several dominant features with large coefficient magnitudes
    - The intercept (β₀) had a negative value, suggesting a baseline bias toward class 0 when feature values are neutral
- **GA with L2 regularization**:
    - Generated weights that achieved the highest test accuracy at 98.83%
    - Showed a similar pattern of feature importance to PSO but with some differences in specific coefficient values
    - Resulted in slightly different weight distribution compared to PSO
- **SA with L2 regularization**:
    - Produced weights yielding 98.25% test accuracy
    - Weight distribution was comparable to PSO and GA
    - Showed consistent performance with the other methods
- **PSO with L1 regularization**:
    - Resulted in sparser weight distribution with more coefficients near zero (9.7% sparsity)
    - Achieved 98.25% test accuracy, comparable to L2 regularization
    - Exhibited stronger feature selection characteristics than L2 regularization


### Which features have large positive/negative coefficients?

Analysis of coefficient magnitudes reveals several features with particularly strong influence on classification:

**Features with large positive coefficients**:

- Feature 6 (mean concavity): Had one of the largest positive coefficients (5.7211 with L2 regularization), suggesting strong association with benign tumors when using L2 regularization
- Several mean texture and symmetry features showed consistent positive weights across different algorithms, indicating these characteristics are associated with benign classification

**Features with large negative coefficients**:

- Feature 18 (worst concave points): Had a large negative coefficient (-2.6850 with L2 regularization), indicating strong association with malignant tumors
- Feature 3 (mean perimeter): Showed a significant negative coefficient (-2.2189 with L2 regularization)
- Feature 1 (mean texture): Demonstrated a stronger negative coefficient with L1 (-3.3929) than with L2 (-1.5370)
- Feature 20 (worst symmetry): Showed interesting regularization-dependent behavior, with L2 yielding 2.3653 and L1 producing -0.1293

These features with large coefficients correspond to specific cell morphology characteristics in the breast cancer dataset that strongly influence the classification decision.

### How does L1 vs. L2 affect the weight distribution?

The comparison between L1 and L2 regularization reveals substantial differences in weight distribution:

- **Sparsity**:
    - L1 regularization resulted in higher sparsity (9.7% coefficients near zero) compared to L2 regularization (6.5%)
    - This confirms the theoretical expectation that L1 promotes feature selection by driving some coefficients to zero
- **Coefficient magnitude**:
    - L1 regularization produced a lower mean absolute coefficient value (1.4884) compared to L2 (1.9379)
    - L2 regularization tends to distribute the penalty across all coefficients, resulting in generally larger but more evenly distributed weights
- **Feature selection effect**:
    - L1 regularization identified a smaller subset of highly influential features
    - L2 regularization maintained contribution from more features, potentially capturing more complex interactions
- **Specific feature differences**:
    - Feature 1: L1 = -3.3929, L2 = -1.5370
    - Feature 3: L1 = 0.2861, L2 = -2.2189
    - Feature 20: L1 = -0.1293, L2 = 2.3653
    - Feature 18: L1 = -0.0486, L2 = -2.6850
    - Feature 6: L1 = 0.9262, L2 = 5.7211

These differences highlight L1's tendency to perform implicit feature selection by pushing less important coefficients toward zero, while L2 tends to preserve contributions from more features but with smaller magnitudes. The visual comparison of coefficient distributions clearly demonstrates these effects.

## D.4 Recommendations

### If you had limited time or computational resources, which method would you pick?

For scenarios with limited time or computational resources, I would recommend **Particle Swarm Optimization (PSO)** for the following reasons:

1. **Consistent performance**: PSO demonstrated reliable convergence behavior with less variability compared to GA and SA, achieving 97.66% test accuracy efficiently.
2. **Implementation simplicity**: PSO has fewer hyperparameters to tune compared to GA, making it more straightforward to implement and adjust. The primary parameter (inertia weight) is intuitive and relatively easy to set.
3. **Computational efficiency**: PSO typically requires fewer function evaluations to reach a good solution compared to GA, which needs to evaluate entire populations across many generations.
4. **Parallelization potential**: If multiple cores are available, PSO's particle evaluations can be easily parallelized to further reduce computation time.
5. **Robustness to initial conditions**: PSO showed less sensitivity to initial particle positions compared to SA's dependence on starting temperature and solution.

While GA achieved slightly higher accuracy (98.83%), the marginal improvement may not justify the additional computational cost and implementation complexity in resource-constrained environments. PSO offers the best balance of simplicity, efficiency, and performance for quick deployment.

### In a high-dimensional feature space, would you expect one method to dominate?

In high-dimensional feature spaces, **Genetic Algorithm (GA)** would likely dominate for several reasons:

1. **Effective global exploration**: GA's crossover operator enables effective jumps across the high-dimensional space, allowing it to explore distant regions more efficiently than PSO or SA.
2. **Implicit dimensionality reduction**: GA naturally focuses on promising subspaces through the selection process, effectively reducing the search dimensionality.
3. **Resilience to curse of dimensionality**: GA's population-based approach maintains diversity even in high dimensions, where distance metrics become less meaningful and can hamper PSO's performance.
4. **Feature subset selection**: In high-dimensional spaces with many irrelevant features, GA's ability to combine good "building blocks" through crossover helps identify useful feature combinations.
5. **Scalable operators**: GA's mutation and crossover operators scale well to high dimensions without requiring specific adaptations.

The experimental results support this expectation, with GA achieving the highest test accuracy (98.83%) even in the moderate-dimensional breast cancer dataset. This advantage would likely become more pronounced as dimensionality increases, particularly in conjunction with L1 regularization for feature selection.

### Summarize your practical tips for selecting a meta-heuristic and setting hyperparameters

Based on the experimental findings, here are practical tips for selecting and configuring meta-heuristic algorithms:

**Algorithm Selection:**

1. **Problem characteristics**: Match the algorithm to the problem - use PSO for continuous, smooth landscapes; GA for combinatorial or discrete problems; SA for problems with many local optima.
2. **Available resources**: Consider PSO for limited computational resources, GA for parallelizable environments, and SA for problems requiring simple implementation.
3. **Problem dimensionality**: For low to moderate dimensions, PSO often provides the best efficiency; for high dimensions, GA typically offers superior performance.
4. **Solution quality vs. speed**: If solution quality is paramount, consider GA with higher population sizes; if speed is critical, PSO or SA with faster cooling may be preferable.

**Hyperparameter Setting:**

1. **PSO configuration**:
    - Start with inertia weight w=0.7 and adjust based on convergence behavior
    - Set cognitive and social constants (c1, c2) equal (around 1.5) initially
    - Use 10-30 particles per dimension for small problems, reducing the ratio for larger problems
2. **GA configuration**:
    - Begin with mutation rate around 0.1 and crossover rate around 0.8
    - Increase mutation rate for complex, high-dimensional problems
    - Population size should scale with problem complexity (50-100 for moderate problems)
3. **SA configuration**:
    - Set initial temperature high enough to accept most moves initially
    - Use cooling rate between 0.9-0.95 for thorough exploration
    - Consider problem-specific step size adaptations for efficient search
4. **Regularization settings**:
    - Use L1 regularization when feature selection is important or interpretability is a priority
    - Use L2 regularization when all features may contribute and smoother weight distribution is desired
    - Start with small regularization parameter (0.01-0.1) and adjust based on validation performance
5. **Monitoring and adaptation**:
    - Track convergence patterns and implement early stopping if progress plateaus
    - Consider adaptive parameter schedules (decreasing inertia in PSO, reducing mutation in GA)
    - Perform sensitivity analysis on key parameters before full-scale optimization