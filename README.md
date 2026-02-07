# Multi-Asset Portfolio Optimisation and Risk Management

This project implements a quantitative portfolio optimisation and risk management framework using historical equity data. The focus is on portfolio construction, optimisation behaviour, and risk mitigation rather than security selection or alpha generation.

Asset selection is based on market prominence and liquidity, without prior fundamental or valuation analysis. Expected returns are estimated from historical price data and may be negative over the sample period. Short selling is permitted to reflect realistic market constraints and to illustrate the theoretical behaviour of unconstrained mean–variance optimisation.

The project includes:
- Mean–variance portfolio optimisation and efficient frontier construction
- Minimum variance and tangency portfolio analysis
- Monte Carlo simulation of portfolio returns using Geometric Brownian Motion
- Downside risk assessment using Value at Risk (VaR)
- Option-based hedging strategies for risk reduction

The results highlight known limitations of classical portfolio optimisation, particularly the sensitivity of tangency portfolios to estimation error in expected returns. These outcomes are discussed explicitly in the report and are intended to demonstrate understanding of both the strengths and weaknesses of the framework.

This project was completed as part of undergraduate studies and is intended as a foundation for further academic work at honours level.
