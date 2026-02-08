# Multi-Asset Portfolio Optimisation and Risk Management

This project implements a quantitative portfolio optimisation and risk management framework using historical equity data. The primary objective is to analyse portfolio construction behaviour and risk characteristics rather than security selection or alpha generation.

Asset selection is based on market prominence and liquidity, without prior fundamental or valuation analysis. Expected returns are estimated from historical price data and may be negative over the sample period. Short selling is permitted to reflect realistic market conditions and to illustrate the theoretical behaviour of unconstrained mean–variance optimisation.

---

## Methodology

### Portfolio Optimisation

Portfolio expected return and variance are defined as:

- Expected portfolio return:  
  E[R_p] = wᵀ μ

- Portfolio variance:  
  σ_p² = wᵀ Σ w

where:
- w is the vector of portfolio weights  
- μ is the vector of expected asset returns  
- Σ is the covariance matrix of asset returns  

The minimum-variance portfolio is obtained by solving:

- Minimise:  
  wᵀ Σ w  
- Subject to:  
  1ᵀ w = 1  

The tangency (maximum Sharpe ratio) portfolio is given by:

- w* ∝ Σ⁻¹ (μ − r_f 1)

where r_f denotes the risk-free rate. Short selling is permitted, resulting in unconstrained solutions.

---

### Risk Simulation

Asset prices are simulated using a Geometric Brownian Motion (GBM):

- dS_t = μ S_t dt + σ S_t dW_t

Simulated asset paths are aggregated to generate a distribution of portfolio returns.

---

### Risk Measurement and Hedging

Downside risk is assessed using Value at Risk (VaR) at confidence level α:

- VaR_α = − inf { x | P(R_p ≤ x) ≥ α }

Option-based hedging strategies are applied to reduce tail risk:
- Long positions are hedged using put options  
- Short positions are hedged using call options  

Options are priced using the Black–Scholes framework.

---

## Key Findings

- Allowing short selling expands the efficient frontier significantly  
- Tangency portfolios exhibit extreme leverage due to sensitivity to expected return estimation  
- Monte Carlo simulations reveal substantial tail risk in unhedged portfolios  
- Option-based hedging materially reduces volatility and Value at Risk, with limited impact on expected return  

These results highlight both the strengths and limitations of classical portfolio optimisation when applied to empirically estimated inputs.

---

## Academic Context

This project was completed as part of undergraduate studies and is intended as a foundation for further academic work at honours level, particularly in the areas of robust optimisation, improved return estimation, and advanced risk modelling.
