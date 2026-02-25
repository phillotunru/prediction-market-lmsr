# Prediction Market LMSR Simulation

A Python project for simulating a prediction market using the LMSR (Logarithmic Market Scoring Rule) market maker. The simulator supports running experiments with fixed ground-truth probabilities, exporting results to CSV/JSON, and analyzing how parameters like risk aversion (`rho`) affect market behavior and final agent positions.

## Overview

This project focuses on an LMSR-based prediction market simulation and includes tools to:

- run market simulations with configurable parameters
- track price convergence over time
- measure error relative to ground truth
- analyze how risk aversion affects final shares/cash
- export results for plotting and analysis

## Setup

Requires Python 3.9+.

```bash
pip install numpy
```

## Run the Simulation

From the repo root:
```
python src/team_a_main.py
```

This runs several LMSR simulation configurations and writes output artifacts to:

```
outputs/
  test1_baseline.json
  test1_baseline_timeseries.csv
  test1_baseline_agents.csv
  test1_baseline_rho_summary.csv
  ...
```


## Output Files

For each run name <run>:

1) <run>_timeseries.csv

Per-round market time series, including:

- price: LMSR market price each round

- abs_error_vs_ground_truth: absolute error |price - P*| per round

- trade_volume: total absolute shares traded in that round

Useful for:

- checking whether price converges toward beliefs / ground truth

- tracking error over time

- analyzing trading activity by round

2) <run>_agents.csv

One row per agent, including:

- rho: risk aversion

- final_shares

- final_cash

Useful for:

- comparing final positions across risk-aversion levels

- analyzing how agent behavior differs by parameter settings

3) <run>_rho_summary.csv

Aggregated statistics by rho, such as:

- avg_shares

- avg_cash

Useful for:

- quickly comparing portfolio outcomes across risk aversion groups

4) <run>.json

Full raw simulation output (includes arrays used to generate CSV exports).

## Parameters

Some key simulation parameters:

- ground_truth (P*): the reference probability used for evaluating error/convergence

- rho: agent risk aversion

b: LMSR liquidity parameter (higher b generally means prices move less per trade)

## Notes

- Ground truth P* is configured in the simulation settings (see src/team_a_phase1_simulation.py).

- Output files are generated automatically after each run and can be used for downstream plotting or analysis.
