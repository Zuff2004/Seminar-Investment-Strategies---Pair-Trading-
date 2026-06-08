# Seminar Investment Strategies - Pair Trading

This repository contains the empirical implementation for the seminar paper:

**ON/PN Relative-Value Strategies in the Brazilian Equity Market:  
A Statistical Arbitrage and Risk Management Approach**

The project was developed for the seminar **Finance & Accounting: Investment Strategies (MGT001517)** at the Technical University of Munich.

## Project Overview

The project investigates whether a long-only ON/PN relative-value rotation strategy can improve risk-adjusted performance in the Brazilian equity market. The strategy reallocates capital between ordinary shares (ON) and preferred shares (PN) of the same company based on rolling z-score deviations of the ON/PN spread.

Unlike traditional long-short pairs trading, the strategy preserves company-level exposure and does not short either share class. It is implemented as a long-only share-class rotation overlay on a fundamentally selected Brazilian equity portfolio.

The final portfolio uses fixed initial company weights. These weights are not rebalanced back to target weights through time; they drift with company-level performance. The active allocation occurs within each company, where the strategy rotates between ON and PN share classes according to the assigned policy.

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

## How to Run

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

Run the final empirical pipeline from the repository root:

```bash
python src/final_main.py
```

The script writes updated tables and plots to `final_results/`.

The optional robustness analysis can be run separately:

```bash
python src/robustness_analysis.py
```

## Repository Structure

```text
src/
    final_main.py                      final baseline pipeline
    robustness_analysis.py             optional sensitivity analysis
    project_config.py                  paths, dates, costs, taxes, universe
    data_loader.py                     Yahoo Finance download and CSV loading
    pair_data.py                       ON/PN/Ibovespa alignment and returns
    universe_filter.py                 statistical pair filtering
    company_policy_engine.py           company-specific policy assignment
    rotation_signal_engine.py          rolling spread z-score target weights
    share_class_rotation_backtester.py trade execution, costs, realized PnL
    individual_tax_account.py          company-level monthly tax helper
    benchmarks.py                      passive 50/50 and Ibovespa benchmarks
    individual_comparison.py           individual result and metric tables
    performance_metrics.py             return, Sharpe, drawdown, hit ratio
    plot_builder.py                    individual and portfolio plots

data/raw/
    cached market data used by the pipeline

final_results/
    generated CSV outputs, performance summaries, robustness results, and plots
