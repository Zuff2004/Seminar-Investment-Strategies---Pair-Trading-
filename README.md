# Seminar Investment Strategies - Pair Trading

This repository contains the empirical implementation for the seminar paper:

**ON/PN Relative-Value Strategies in the Brazilian Equity Market:  
A Statistical Arbitrage and Risk Management Approach**

The project was developed for the seminar **Finance & Accounting: Investment Strategies (MGT001517)** at the Technical University of Munich.

## Project Overview

The project investigates whether a long-only ON/PN relative-value rotation strategy can improve risk-adjusted performance in the Brazilian equity market. The strategy reallocates capital between ordinary shares (ON) and preferred shares (PN) of the same company based on rolling z-score deviations of the ON/PN spread.

Unlike traditional long-short pairs trading, the strategy preserves company-level exposure and does not short either share class. It is implemented as a long-only share-class rotation overlay on a fundamentally selected Brazilian equity portfolio.


## Main Features

- Construction of an ON/PN Brazilian equity universe
- Fundamental screening based on FY2019 company indicators
- Statistical filtering using correlation, spread volatility, cointegration, and ADF tests
- Company-specific ON/PN rotation policies
- Rolling z-score signal generation
- Quantity-based backtesting
- Transaction cost modelling
- Portfolio-level monthly tax treatment with loss carryforward
- Benchmark comparison against:
  - Passive 50/50 ON/PN portfolio
  - Statistical-only equal-weighted portfolio
  - Ibovespa
- Robustness and sensitivity analysis
- Company-level and portfolio-level result exports

## Final Results

The final strategy is evaluated from January 2020 to December 2025.  
The implemented after-tax portfolio achieves:

| Metric | Final Strategy |
|---|---:|
| Total return after tax | 123.97% |
| Annualized return | 14.57% |
| Sharpe ratio | 0.6874 |
| Maximum drawdown | -42.63% |

The strategy outperforms the passive 50/50 ON/PN benchmark and the Ibovespa over the same out-of-sample period.

## Repository Structure

```text
src/
    data loading, filtering, policy engine, backtesting, portfolio construction

final_results/
    generated CSV outputs, performance summaries, robustness results, and plots

paper/
    final seminar paper and supporting LaTeX files