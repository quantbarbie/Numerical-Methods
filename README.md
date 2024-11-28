# **1. Arbitrage-Free Smile Interpolator**

## **Project Overview**
This project involves implementing an arbitrage-free smile interpolator to enhance pricing accuracy and eliminate arbitrage opportunities.

### **Key Objectives**
1. Implement an arbitrage-free smile interpolator (`SmileAF`).
2. Construct a local volatility model using the interpolator.
3. Use a PDE-based approach to price European options with the local volatility model.
4. Compare pricing errors of the arbitrage-free interpolator with cubic spline interpolators.
5. Explore further improvements for precision and efficiency, particularly in tail construction.

---

## **Features**

### **Arbitrage-Free Smile**
- Ensures monotonicity and convexity of European call prices.
- Guarantees non-negative probability density (butterfly prices).

### **Local Volatility Model**
- Derives a local volatility surface from implied volatility data.
- Uses cubic spline interpolation to ensure smooth volatility surfaces.

### **PDE Pricing**
- Efficiently prices European options using the local volatility surface.

### **Comparison**
- Evaluates calibration errors for different smile interpolation methods.

---

## **Implementation**

### **SmileAF: Arbitrage-Free Smile Interpolator**
The `SmileAF` class ensures an arbitrage-free volatility surface by:
1. Constructing call price functions with monotonicity and convexity constraints.
2. Using quadratic programming to solve for smooth probability densities.
3. Providing seamless interpolation of implied volatilities.

#### **Key Constraints**
1. Monotonicity and convexity of call prices.
2. Non-negative density functions.
3. Exact fit to given strike-volatility marks.
4. Spline interpolation for smoothness.

#### **Optimization Methodology**
- Quadratic programming (`CVXOPT`) ensures precision.
- Smooth extrapolation for tail handling.

---

## **Usage**

### **Inputs**
- Strike-volatility pairs (`k`, `σ`).
- Other parameters such as forward price, interest rates, and maturities.

### **Outputs**
- Arbitrage-free volatility surface.
- European option prices derived from the local volatility model.

---

## **Testing**

### **Test Scenarios**
1. **Flat Volatility Surface**:
   - Baseline testing with no smile.
2. **Smile with Cubic Spline**:
   - Mild and strong smiles to test cubic spline performance.
3. **Arbitrage-Free SmileAF**:
   - Evaluates performance without arbitrage issues.

### **Visualization**
- Implied volatility surface plots.
- Calibration error heatmaps.

## **Comparison and Conclusion**

### **Cubic Spline vs Arbitrage-Free Interpolator**

#### **Cubic Spline**
- Larger calibration errors in short-end, low-strike regions.
- Prone to arbitrage with inconsistent market data.

#### **Arbitrage-Free SmileAF**
- Reduces mispricing by enforcing non-arbitrage constraints.
- Improves hedging performance.

---

### **Advantages of Arbitrage-Free Interpolation**
- Handles inconsistent data without introducing arbitrage.
- Produces smooth and stable volatility surfaces.
- Ensures better convergence in PDE pricing.

---

## **Improvement Suggestions**
1. Implement parametric models to handle extreme moneyness and maturity values.
2. Incorporate level, slope, and curvature factors for better interpolation.
3. Ensure twice-continuous differentiability for smoother risk-neutral density estimation.

---

## **References**
- [Fengler, 2009] *Arbitrage-Free Smoothing of the Implied Volatility Surface*, Quantitative Finance.

## **2. Homework 1, Option pricing**

### **Function Description**
A function to convert `fixed<w, b>` representation to a real number using two's complement representation for negative numbers.
`# CRR Binomial Tree Model and Greeks Calculation

## 2. CRR Binomial Tree Model

The **Cox-Ross-Rubinstein (CRR)** binomial tree model is a discrete-time approach for option pricing. It evaluates the possible paths of an option's price iteratively.

### Function Signature

def eurocall_crr(S, K, r, T, sigma, n): 

### Parameters

-   **S**: Initial stock price.
-   **K**: Strike price.
-   **r**: Risk-free interest rate.
-   **T**: Time to maturity (in years).
-   **sigma**: Volatility of the stock.
-   **n**: Number of time steps in the binomial tree.

* * * * *

3\. Binomial Tree Models
------------------------

### Implemented Models

-   **CRR** (Cox-Ross-Rubinstein)
-   **JRRN** (Jarrow-Rudd Natural Measure)
-   **JREQ** (Jarrow-Rudd Equal Measure)
-   **Tian Calibration**

### Functionality

The binomial tree models are used to calculate the prices of financial derivatives (European call and put options). Each model uses its unique calibration for the upward and downward movement factors.

* * * * *

4\. Greeks Calculator
---------------------

### Overview

Greeks measure the sensitivity of derivative prices to changes in underlying parameters. The following Greeks are calculated:

-   **Delta (Δ\DeltaΔ)**: Sensitivity to underlying price changes.
-   **Gamma (Γ\GammaΓ)**: Rate of change of Delta.
-   **Vega (vvv)**: Sensitivity to volatility changes.
-   **Theta (θ\thetaθ)**: Sensitivity to time decay.
-   **Rho (ρ\rhoρ)**: Sensitivity to interest rate changes.

### Finite Difference Approximations

The Greeks are approximated using the following formulas:

1.  **Delta (Δ\DeltaΔ)**:

    Δ≈V(S+ΔS)-V(S-ΔS)2ΔS,ΔS=0.1%×S\Delta \approx \frac{V(S + \Delta S) - V(S - \Delta S)}{2 \Delta S}, \quad \Delta S = 0.1\% \times SΔ≈2ΔSV(S+ΔS)-V(S-ΔS)​,ΔS=0.1%×S
2.  **Gamma (Γ\GammaΓ)**:

    Γ≈V(S+ΔS)-2V(S)+V(S-ΔS)ΔS2\Gamma \approx \frac{V(S + \Delta S) - 2V(S) + V(S - \Delta S)}{\Delta S^2}Γ≈ΔS2V(S+ΔS)-2V(S)+V(S-ΔS)​
3.  **Vega (vvv)**:

    v≈V(σ+Δσ)-V(σ-Δσ)2Δσ,Δσ=0.1%v \approx \frac{V(\sigma + \Delta \sigma) - V(\sigma - \Delta \sigma)}{2 \Delta \sigma}, \quad \Delta \sigma = 0.1\%v≈2ΔσV(σ+Δσ)-V(σ-Δσ)​,Δσ=0.1%
4.  **Theta (θ\thetaθ)**:

    θ≈V(t+Δt)-V(t)Δt,Δt=0.004\theta \approx \frac{V(t + \Delta t) - V(t)}{\Delta t}, \quad \Delta t = 0.004θ≈ΔtV(t+Δt)-V(t)​,Δt=0.004
5.  **Rho (ρ\rhoρ)**:

    ρ≈V(r+Δr)-V(r-Δr)2Δr,Δr=0.0001\rho \approx \frac{V(r + \Delta r) - V(r - \Delta r)}{2 \Delta r}, \quad \Delta r = 0.0001ρ≈2ΔrV(r+Δr)-V(r-Δr)​,Δr=0.0001


### Supported Models

-   **greeks_crr**: Greeks calculation for CRR model.
-   **greeks_jrrn**: Greeks calculation for JRRN model.
-   **greeks_jreq**: Greeks calculation for JREQ model.
-   **greeks_tian**: Greeks calculation for Tian model.
