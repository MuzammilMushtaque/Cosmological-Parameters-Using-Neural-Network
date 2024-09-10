# Estimating Cosmological Parameters with an Artificial Neural Network

### Introduction:

**Goal:** Develop a neural network model to estimate $\Omega_{matter}$ (dark matter density parameter) and the Hubble constant ($H_0$) by analyzing the relationship between Hubble values and redshift (z).

**Data Generation:**

* **Friedmann Equation:**
  
$\
  H(z) = H_0 \cdot \sqrt{\Omega_m \cdot (1 + z)^3 + \Omega_\Lambda}
\$

* **Assumptions:**
  * Radiation density parameter ($\Omega_r$) is assumed to be 0.
  * $\Omega_\Lambda = 1 - \Omega_m$
* **Data Generation Process:**
  * Generate synthetic data for Hubble values using the Friedmann equation.
  * Add noise to the data based on residuals from observational versus theoretical values.
  * Vary Hubble constant $H_0$, $\Omega_m$ across a range of possible values to create a comprehensive dataset.
