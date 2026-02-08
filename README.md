# Multi-Asset Portfolio Optimisation and Risk Management

This project implements a quantitative portfolio optimisation and risk management framework using historical equity data. The primary objective is to analyse portfolio construction behaviour and risk characteristics only.

Asset selection is based on market prominence and liquidity, without prior fundamental or valuation analysis. Expected returns are estimated from historical price data and may be negative over the sampled period. Short selling is permitted to reflect realistic market conditions and to illustrate the theoretical behaviour of unconstrained mean–variance optimisation.

---

## Methodology

### Portfolio Optimisation

Portfolio expected return and variance are defined as:

* **Expected portfolio return:** $$E[R_p] = \mathbf{w}^T \boldsymbol{\mu}$$

* **Portfolio variance:** $$\sigma_p^2 = \mathbf{w}^T \boldsymbol{\Sigma} \mathbf{w}$$

where:
* $\mathbf{w}$ is the vector of portfolio weights  
* $\boldsymbol{\mu}$ is the vector of expected asset returns  
* $\boldsymbol{\Sigma}$ is the covariance matrix of asset returns  

The minimum-variance portfolio is obtained by solving:

* **Minimise:** $$\mathbf{w}^T \boldsymbol{\Sigma} \mathbf{w}$$
* **Subject to:** $$\mathbf{1}^T \mathbf{w} = 1$$

The tangency (maximum Sharpe ratio) portfolio is given by:

$$\mathbf{w}^* \propto \boldsymbol{\Sigma}^{-1} (\boldsymbol{\mu} - r_f \mathbf{1})$$

where $r_f$ denotes the risk-free rate. Short selling is permitted, resulting in unconstrained solutions.

---

### Risk Simulation

Asset prices are simulated using a Geometric Brownian Motion:

$$dS_t = \mu S_t dt + \sigma S_t dW_t$$

Simulated asset paths are aggregated to generate a distribution of portfolio returns.

---

### Risk Measurement and Hedging

Downside risk is assessed using Value at Risk (VaR) at confidence level $\alpha$:

$$VaR_\alpha = -\inf \{ x \mid P(R_p \leq x) \geq \alpha \}$$

Option-based hedging strategies are applied to reduce tail risk:
* Long positions are hedged using put options  
* Short positions are hedged using call options  

Options are priced using the Black–Scholes framework.

---

## Remarks

* Allowing short selling expands the efficient frontier significantly  
* Tangency portfolios exhibit extreme leverage due to sensitivity to expected return estimation  
* Monte Carlo simulations reveal tail risk in unhedged portfolios  
* Option-based hedging reduces volatility and Value at Risk, with limited impact on expected return  

These results highlight both the strengths and limitations of classical portfolio optimisation when applied to empirically estimated inputs.
