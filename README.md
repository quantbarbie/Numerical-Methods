# **Arbitrage-Free Smile Interpolator**

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

