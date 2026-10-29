# Temporal Dynamics of Goal Scoring in the English Premier League (2020 to 2025)

Final project for DACSS 790D: Temporal Dynamics (UMass Amherst, Spring 2026).

This project models weekly average goal scoring in the Premier League across five seasons and tests whether adding expected goals (xG) to an ARIMA model improves forecasts over a univariate baseline.

**[View the full report (HTML)](790D_final_project.html)**

## Data

- [`final_matches.csv`](final_matches.csv): 3,800 match-level records from FBref.com, covering every Premier League fixture from September 2020 to May 2025 (27 clubs)
- Aggregated into 169 weekly observations (weeks with at least 5 matches)
- Train: first four seasons. Test: the full 2024/25 season (38 weeks)

## Methods

- STL decomposition (seasonal period of 38 matchweeks)
- Stationarity checks with ADF and KPSS tests
- ACF and PACF analysis for model order selection
- ARIMA(1,0,2) baseline vs. ARIMA(1,0,2) with xG as an exogenous regressor
- Residual diagnostics (Ljung-Box, Shapiro-Wilk, heteroskedasticity)
- Out-of-sample evaluation with RMSE and MAE

## Key Results

| Model | AIC | Test RMSE | Test MAE |
|---|---|---|---|
| ARIMA(1,0,2) baseline | 56.69 | 0.330 | 0.261 |
| ARIMA(1,0,2) with xG | 11.66 | 0.165 | 0.131 |

- Adding xG cut forecast error roughly in half
- The xG coefficient (1.036) is close to 1, so xG tracks actual goals almost one to one at the weekly level
- Goal scoring trended upward from 2020/21 to a peak in 2023/24, then eased in 2024/25
- Home win rate has not settled back to its historical norm of around 43 percent since the no-fans 2020/21 season

## Repository Structure

```
.
├── 790D_final_project.qmd    # Quarto source (R code + write-up)
├── 790D_final_project.html   # Rendered, self-contained report
├── final_matches.csv         # Match-level data from FBref
└── README.md
```

## Reproducing the Analysis

Requires R and [Quarto](https://quarto.org/).

```r
install.packages(c("tidyverse", "lubridate", "forecast", "tseries",
                   "strucchange", "modelsummary", "knitr", "kableExtra",
                   "scales"))
```

Clone the repo and render from the project folder (the data file is already included):

```bash
quarto render 790D_final_project.qmd
```

## Author

Nachiketh Kadkol
