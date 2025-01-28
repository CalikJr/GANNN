# Genetic Algorithm + Nonlinear Neural Network for Portfolio Optimization

This repository contains the implementation of a **Genetic Algorithm (GA)** combined with a **Nonlinear Neural Network (NNN)** for solving the portfolio optimization problem. The project was developed as part of a **Genetic Algorithm coursework**, and its methodology was inspired by the ideas presented in the research paper:

**A hybrid approach to cardinality constraint portfolio selection problem
based on nonlinear neural network and genetic algorithm**

---

## **Project Overview**

The objective of this project is to construct an optimal portfolio by selecting a subset of assets and fine-tuning their weights to minimize risk and maximize return. The optimization problem is solved in two stages:

1. **Asset Selection Using Genetic Algorithm (GA):**
   - The GA searches for the best subset of assets (\( z_i \)), where each chromosome in the population represents a binary vector indicating whether an asset is included in the portfolio.
   - Fitness is evaluated based on the portfolio's Sharpe Ratio, computed using fine-tuned weights from the NNN.

2. **Weight Fine-Tuning Using Nonlinear Neural Network (NNN):**
   - For the selected subset of assets, the NNN is trained to adjust portfolio weights (\( x_i \)).
   - The model minimizes portfolio risk (variance) while satisfying the budget constraint (\( \sum x_i = 1 \)) and the target return constraint (\( \sum x_i \mu_i \geq R^* \)).
   - The Lagrangian-based loss function enforces these constraints.

---

## **Key Features**

- **Genetic Algorithm:**
  - Asset selection is optimized using a GA with standard operators:
    - **Selection:** Tournament selection based on fitness (Sharpe Ratio).
    - **Crossover:** Single-point crossover for generating offspring.
    - **Mutation:** Random flipping of bits in chromosomes to introduce variability.
  - Ensures only a fixed number of assets (\( K \)) are selected in the final portfolio.

- **Nonlinear Neural Network:**
  - A fully connected feedforward neural network fine-tunes portfolio weights.
  - Ensures non-negative weights and normalization (\( x_i \geq 0, \sum x_i = 1 \)).
  - Trained using a Lagrangian loss function incorporating portfolio risk and constraints.

- **Real Financial Data:**
  - Utilizes historical stock price data fetched from **Yahoo Finance** (via the `yfinance` library).
  - Calculates daily returns, mean returns, and covariance matrix for portfolio optimization.

---

## **How It Works**

1. **Data Acquisition:**
   - Historical adjusted close prices for selected stocks are fetched using `yfinance`.
   - Daily returns, mean returns, and covariance matrices are computed from the data.

2. **Genetic Algorithm:**
   - A binary chromosome of length \( N \) (number of assets) is initialized.
   - Each chromosome encodes whether an asset is included in the portfolio (1) or not (0).
   - Fitness is evaluated as the Sharpe Ratio of the portfolio, computed using weights optimized by the NNN.

3. **Neural Network Training:**
   - For each chromosome (selected assets), a dedicated NNN is initialized and trained.
   - The Lagrangian-based loss function enforces:
     - Budget Constraint: \( \sum x_i = 1 \)
     - Target Return Constraint: \( \sum x_i \mu_i \geq R^* \)

4. **Portfolio Optimization Output:**
   - The best chromosome (asset selection) and corresponding weights are used to construct the optimal portfolio.
   - Metrics like expected return, risk, and Sharpe Ratio are provided for the final portfolio.

---

## **Requirements**

- Python 3.8 or higher
- Libraries:
  - `numpy`
  - `pandas`
  - `torch` (PyTorch)
  - `yfinance`

Install dependencies using:
```bash
pip install -r requirements.txt
