# Structural Industrial Organization: Demand & Production Estimation

## 📌 Project Overview
This repository contains a comprehensive econometric analysis of market dynamics, split into two major components: **Demand-side estimation** (using Discrete Choice Models) and **Supply-side estimation** (using Production Functions).

 The project demonstrates the application of structural econometric techniques to correct for endogeneity bias, simultaneity, and selection bias using Python.

## 🛠 Tech Stack & Tools
* **Languages:** Python (3.11+)
* **Econometrics:** `pyblp` (Berry-Levinsohn-Pakes), `pyfixest` (High-dimensional fixed effects).
* **Data Manipulation:** `pandas`, `numpy`.
* **Optimization & Stats:** `scipy.optimize`, `scipy.stats`.
* **Visualization:** `seaborn`, `matplotlib`.

---

## 📊 Part 1: Demand Estimation (Cable TV Market)
**Objective:** Estimate consumer preferences for Satellite vs. Wired TV services while correcting for price endogeneity.

### Methodologies Applied:
1.  **OLS & Plain Logit:** Baseline estimation. Results showed attenuation bias (coefficients close to zero) due to the correlation between price and unobserved quality ($\xi$).
2.  **Instrumental Variables (IV):** Used cost-shifters/Hausman instruments. Resulted in $| \beta_{IV} | > | \beta_{OLS} |$, confirming that OLS underestimated price sensitivity.
3.  **Nested Logit:** Tested for correlation within groups (Satellite vs. Wired). The nesting parameter $\rho$ was found to be close to zero, suggesting weak correlation within nests.
4.  **Mixed Logit (Random Coefficients):** Modeled heterogeneity in consumer preferences.

### Key Insights:
* **Bias Correction:** The price coefficient shifted from $\approx -1.09$ (OLS) to $\approx -1.99$ (IV), effectively correcting for endogeneity.
* **Preference Heterogeneity:** The Mixed Logit model revealed a higher variance in utility for **Wired** services ($\sigma \approx 3.24$) compared to Satellite ($\sigma \approx 0$). This suggests polarized consumer experiences with wired cable (likely due to varying local infrastructure quality), whereas Satellite service quality is nationally uniform.
* **Substitution Patterns:** Cross-price elasticities were calculated, showing that products are substitutes, but the substitution patterns are driven more by random coefficients than by nesting structures.

---

## 🏭 Part 2: Supply Estimation (Production Function)
**Objective:** Estimate Total Factor Productivity (TFP) for firms, correcting for simultaneity and endogenous exit.

### Methodologies Applied:
1.  **Olley-Pakes (OP) Estimator:** Used investment as a proxy for unobserved productivity shocks to solve the simultaneity problem.
2.  **Correction for Endogenous Exit:** Modeled firm survival probability using a **Probit model** and incorporated it into the second stage of the OP algorithm to correct for selection bias.
3.  **Bootstrapping:** Implemented a firm-level clustered bootstrap to compute robust standard errors and confidence intervals for production coefficients.

### Key Insights:
* **Input Elasticities:**
    * Labor ($\alpha_L$): $\approx 0.59$
    * Capital ($\alpha_K$): $\approx 0.31$ (with exit correction) vs $\approx 0.35$ (standard OP).
* **Selection Bias:** Correcting for endogenous exit lowered the capital coefficient. This aligns with theory: failing to account for exiting firms (who likely have lower capital/productivity) leads to an overestimation of capital's contribution.
* **Returns to Scale:** The sum of coefficients ($\alpha_L + \alpha_K \approx 0.9$) suggests slightly decreasing to constant returns to scale.

---

## 📈 Part 3: Productivity Analysis
Derived **Total Factor Productivity (TFP)**, denoted as $\hat{\omega}_{it}$, for each firm.

* **Analysis:** Investigated the relationship between productivity and firm exit.
* **Finding:** Contrary to standard "cleansing effect" theories, the data showed that higher productivity did not strictly guarantee lower exit rates in this specific sample. This suggests that exit decisions might be driven by factors other than pure technological efficiency (e.g., demand-side shocks or fixed costs).

---

## 🚀 How to Run
1. Clone the repository.
2. Install dependencies: `pip install pyblp pyfixest`.
3. Run `merged.ipynb`.
