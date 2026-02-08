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

## Sensitivity Analysis

### Sensitivity of the Tangency Portfolio to the Risk-Free Rate

Mean–variance optimisation is known to be highly sensitive to input assumptions, particularly the risk-free rate used in the construction of the tangency portfolio. To assess the robustness of the results, a sensitivity analysis is conducted by varying the annual risk-free rate over a wide range and recalculating the tangency portfolio weights, expected return, volatility, and Sharpe ratio at each level.

The tangency portfolio weights are defined as:

$$\mathbf{w}^*(r_f) \propto \boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu} - r_f \mathbf{1})$$

As the risk-free rate increases, the excess return vector $(\boldsymbol{\mu} - r_f \mathbf{1})$ shrinks and eventually changes sign, causing substantial changes in portfolio composition.



### Outcomes

1. **Existence of a Critical Risk-Free Rate** The analysis reveals a critical region around $r_f \approx 7.8\% – 8.06\%$, where the behaviour of the tangency portfolio changes abruptly:
   - At $r_f \approx 7.8\%$, the expected tangency portfolio return reaches its maximum (approx. 28.5%).
   - Beyond this point, a marginal increase in the risk-free rate causes the expected return to collapse sharply, reaching a trough (approx. −94.56%) at $r_f \approx 8.06\%$.

2. **Instability of Portfolio Weights** Portfolio weights exhibit extreme sensitivity in the same region. Asset weights increase rapidly in magnitude as the optimiser attempts to compensate for declining excess returns. Around the critical threshold, several asset positions flip sign (long to short and vice versa).

3. **Sharpe Ratio Sign Reversal** The Sharpe ratio transitions from positive to negative over the same range:
   - At $r_f \approx 7.8\%$, the Sharpe ratio remains positive (approx. 0.127).
   - At $r_f \approx 8.06\%$, it becomes negative (approx. −0.127).
   A negative Sharpe ratio implies the portfolio underperforms the risk-free asset.

4. **Volatility Explosion** Portfolio volatility exhibits nonlinear behaviour. Volatility initially increases moderately as leverage rises, then explodes near the critical threshold, peaking at approximately **740%**. 

---

### Risk Simulation

Asset prices are simulated using a Geometric Brownian Motion (GBM):

$$dS_t = \mu S_t dt + \sigma S_t dW_t$$



Simulated asset paths are aggregated to generate a distribution of portfolio returns.

---

### Risk Measurement and Hedging

Downside risk is assessed using Value at Risk (VaR) at confidence level $\alpha$:

$$VaR_\alpha = -\inf \{ x \mid P(R_p \leq x) \geq \alpha \}$$

Option-based hedging strategies are applied to reduce tail risk:
* **Long positions** are hedged using put options  
* **Short positions** are hedged using call options  

Options are priced using the Black–Scholes framework.

---

## Remarks

* **Short Selling:** Allowing short selling expands the efficient frontier significantly.
* **Sensitivity:** Tangency portfolios exhibit extreme leverage due to sensitivity to expected return estimation.
* **Monte Carlo:** Simulations reveal significant tail risk in unhedged portfolios.
* **Hedging:** Option-based hedging reduces volatility and Value at Risk with limited impact on expected return.

These results highlight both the strengths and limitations of classical portfolio optimisation when applied to empirically estimated inputs.
