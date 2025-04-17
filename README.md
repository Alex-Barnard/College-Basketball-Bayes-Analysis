# 🏀 College Basketball Bayesian Data Analysis

This project uses Bayesian logistic regression to estimate the probability that a college basketball team reaches the **Final Four** based on key efficiency metrics such as **Adjusted Offensive Efficiency (AdjOE)**, **Adjusted Defensive Efficiency (AdjDE)**, **Efficiency Margin (AdjEM)**, and **Tempo**. The model includes a hierarchical component for team **seed**, acknowledging variability in team strength.

## 📋 Prerequisites

Before running the project, ensure you have the following installed:

- R (≥ 4.0)
- RStudio
- Required R packages:
  - `tidyverse`
  - `dagitty`
  - `ggdag`
  - `ggplot2`
  - `bayesplot`
  - `rethinking`
  - `rstan`

> You can install missing packages using:

```r
install.packages(c("tidyverse", "dagitty", "ggdag", "ggplot2", "bayesplot"))
remotes::install_github("rmcelreath/rethinking")

🚀 How to Run the Project

Follow these steps to reproduce the analysis:

Step 1: Open the Project
	Launch RStudio
	Open the file College_Basketball_Data_Analysis.qmd

Step 2: Load and Inspect the Data
	The CSV file summary25_pt.csv is loaded using read_csv()
	Run the glimpse(data) chunk to understand variable structure

Step 3: Preprocess the Data
	The binary outcome final_four is created to indicate whether a team reached the Final Four
	Predictors such as AdjOE, AdjDE, AdjEM, and AdjTempo are standardized using scale()

Step 4: Visualize the Causal Assumptions
	A DAG (Directed Acyclic Graph) is constructed using dagitty and ggdag to clarify variable relationships

Step 5: Define the Model
	A logistic regression model is specified using ulam() with:
	Fixed effects for the four main predictors
	A group-level (hierarchical) intercept for seed
	Priors:
	Coefficients: Normal(0, 1.5)
	Seed effects: Normal(0, sigma_seed)
	sigma_seed ~ Exponential(1)

Step 6: Run the Model
	Fit the model using ulam()
	Run precis(m_mcmc, depth = 2) to view posterior summaries

Step 7: Diagnose and Interpret
	Optionally, run traceplot(m_mcmc) for convergence diagnostics
	Use postcheck(m_mcmc) or sim for posterior predictive checks
	Interpret the estimates from precis() and relate them back to tournament performance

📊 Research Question

What is the probability that a team reaches the Final Four based on their adjusted offensive and defensive efficiency?

This analysis helps identify key metrics that predict success and provides insights useful for fans, analysts, and sports statisticians.

📌 Notes
	This project is implemented using the Bayesian framework and leverages ulam() from the rethinking package.
	All predictors are scaled for better interpretability and to assist in prior selection.
	The hierarchical structure improves the model by accounting for variability across seed rankings.



📚 References
	Gelman, Andrew, et al. Bayesian Data Analysis. 3rd ed., CRC Press, 2013.
	McElreath, Richard. Statistical Rethinking: A Bayesian Course with Examples in R and Stan. 2nd ed., CRC Press, 2020.
  



🤝 Acknowledgements

This project is developed as part of a Bayesian modeling course (STAT 341). Special thanks to the instructor and course materials for guidance.



🔁 Future Extensions
	Compare Bayesian model performance with a frequentist logistic regression
	Incorporate more predictors (e.g., player stats, team wins)
	Explore predictive modeling using new data from the 2024 tournament
