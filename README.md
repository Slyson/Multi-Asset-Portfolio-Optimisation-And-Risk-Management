# Multi-Asset Portfolio Optimisation and Risk Management

This project implements a quantitative portfolio optimisation and risk management framework using historical equity data. The primary objective is to analyse portfolio construction behaviour and risk characteristics rather than security selection or alpha generation.

Asset selection is based on market prominence and liquidity, without prior fundamental or valuation analysis. Expected returns are estimated from historical price data and may be negative over the sample period. Short selling is permitted to reflect realistic market conditions and to illustrate the theoretical behaviour of unconstrained mean–variance optimisation.

---

## Methodology

### Portfolio Optimisation

Portfolio weights are determined using classical mean–variance optimisation. Portfolio return and variance are defined as:

\[
\mathbb{E}[R_p] = \mathbf{w}^\top \boldsymbol{\mu}
\]

\[
\sigma_p^2 = \mathbf{w}^\top \boldsymbol{\Sigma} \mathbf{w}
\]

where:
- \(\mathbf{w}\) is the vector of portfolio weights  
- \(\boldsymbol{\mu}\) is the vector of expected asset returns  
- \(\boldsymbol{\Sigma}\) is the covariance matrix of asset returns  

The minimum-variance portfolio is obtained by solving:

\[
\min_{\mathbf{w}} \ \mathbf{w}^\top \boldsymbol{\Sigma} \mathbf{w}
\quad \text{subject to} \quad \mathbf{1}^\top \mathbf{w} = 1
\]

The tangency (maximum Sharpe ratio) portfolio is defined as:

\[
\mathbf{w}^* \propto \boldsymbol{\Sigma}^{-1} (\boldsymbol{\mu} - r_f \mathbf{1})
\]

where \(r_f\) is the risk-free rate. Short selling is allowed, resulting in unconstrained solutions.

---

### Risk Simulation

Portfolio risk is analysed using Monte Carlo simulation under a Geometric Brownian Motion (GBM) assumption:

\[
dS_t = \mu S_t \, dt + \sigma S_t \, dW_t
\]

Simulated asset paths are aggregated to generate a distribution of portfolio returns, from which downside risk metrics are computed.

---

### Risk Measurement and Hedging

Downside risk is assessed using Value at Risk (VaR), defined at confidence level \(\alpha\) as:

\[
\text{VaR}_\alpha = - \inf \{ x \mid P(R_p \le x) \ge \alpha \}
\]

Option-based hedging strategies are applied to reduce tail risk:
- Long positions are hedged using put options
- Short positions are hedged using call options

Options are priced using the Black–Scholes framework.

---

## Key Findings

- Efficient frontiers expand significantly when short selling is permitted
- Tangency portfolios exhibit extreme leverage due to sensitivity to expected return estimation
- Monte Carlo simulations highlight substantial tail risk in unhedged portfolios
- Option-based hedging materially reduces volatility and Value at Risk, with limited impact on expected return

These outcomes illustrate both the strengths and limitations of classical portfolio optimisation when applied to empirically estimated inputs.

---

## Academic Context

This project was completed as part of undergraduate studies and is intended as a foundation for further academic work at honours level, particularly in the areas of robust optimisation, improved return estimation, and advanced risk modelling.
