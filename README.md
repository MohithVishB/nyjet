# Jets Target Efficiency (Context-Adjusted EPA)

This repository analyzes New York Jets pass targets using context-adjusted EPA, cross-fitted modeling, and receiver-by-bucket evaluation.

## Overview
This project builds a league-wide baseline model to estimate expected EPA for every target. Jets targets are evaluated by comparing observed EPA to expected EPA, producing residuals that measure performance relative to situation and target difficulty.

The workflow includes:
- League baseline model (RidgeCV)
- Out-of-fold expected EPA via GroupKFold
- Residual EPA computation
- Target bucketing by depth and direction
- Shrinkage correction
- Bootstrap uncertainty intervals
- CI-filtered recommendations
- Numerical reallocation estimate

## Bucket Structure
Depth buckets:
- short (<= 5 air yards)
- intermediate (6–15)
- deep (>= 16)

Direction buckets:
- left
- middle
- right

These combine to form 9 depth-direction target buckets.

## Key Results (2025 Season)
Baseline model performance:
- MAE: 1.13
- R²: 0.02

Team-level findings:
- Best bucket: short_right
- Weakest bucket: deep_middle

CI-filtered actionable recommendations:
- Increase: M. Taylor — intermediate_left
- Decrease: A. Mitchell — intermediate_right

Reallocation estimate:
- Shifting 4 targets per game yields approximately +1.72 EPA per game

## How to Run
Install dependencies:
```
pip install nfl_data_py scikit-learn pandas numpy matplotlib seaborn
```

Steps:
1. Load play-by-play data
2. Build the baseline model
3. Generate out-of-fold expected EPA
4. Compute residuals
5. Aggregate receiver-by-bucket results
6. Apply shrinkage and bootstrap
7. Export tables and recommendations
