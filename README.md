---
title: "ReadMe"
format: gfm
jupyter: python3
---
# The “Caitlin Clark Effect” on WNBA Attendance

## Table of Contents

* [Project Overview](#project-overview)
* [Research Motivation](#research-motivation)
* [Research Questions](#research-questions)
* [Data Sources](#data-sources)
* [Tools and Libraries](#tools-and-libraries)
* [Data Collection](#data-collection)
* [Data Wrangling and Feature Engineering](#data-wrangling-and-feature-engineering)
* [Modeling Approach](#modeling-approach)
* [Results](#results)
* [Model Interpretation](#model-interpretation)
* [Key Takeaways](#key-takeaways)
* [Limitations](#limitations)
* [Future Work](#future-work)
* [References](#references)

---

## Project Overview

This project investigates the **“Caitlin Clark Effect”** — the impact of Caitlin Clark’s presence on WNBA game attendance. Building on existing research documenting Clark’s influence during her collegiate career, this analysis extends the question to the professional level to determine whether a single athlete can meaningfully drive fan engagement in a professional women’s sports league.

The project places heavy emphasis on data integration, feature engineering, and model interpretability, using multiple statistical and machine-learning approaches to evaluate attendance drivers.

---

## Research Motivation

Women’s sports have experienced rapid growth in recent years, and the WNBA has reported record-breaking attendance and viewership. Understanding whether star players like Caitlin Clark directly contribute to this growth is valuable for:

* League-level marketing strategy
* Team revenue optimization
* Media rights negotiation
* Broader investment in women’s athletics

This project explores whether Caitlin Clark’s presence produces a measurable and statistically significant impact on WNBA attendance.

---

## Research Questions

1. Does Caitlin Clark’s presence increase WNBA game attendance?
2. How does her professional impact compare to her college influence?
3. Which modeling approach best captures attendance dynamics in the WNBA?

---

## Data Sources

The analysis combines multiple datasets:

* WeHoop Library (2022–2025 WNBA Seasons)

  * Player-level and game-level statistics
  * Minutes played, points scored, three-point shots made
* Across the Timeline – Women’s Basketball Data

  * Game-level attendance data by city and venue

The final cleaned dataset contains 1,046 rows and 18 engineered features.

---

## Tools and Libraries

* Python
* Pandas – data manipulation and merging
* Scikit-learn – linear regression, bagging, GridSearchCV
* XGBoost – nonlinear predictive modeling
* SHAP – model explainability
* Matplotlib / Seaborn – visualizations
* Jupyter Notebook – reproducible analysis

---

## Data Collection

* WNBA player and game data were sourced using the WeHoop library
* Attendance data was collected from Across the Timeline
* Dates were standardized to allow clean merges
* A binary indicator (`Caitlin_played`) was manually created to flag games in which Clark appeared

---

## Data Wrangling and Feature Engineering

Key preparation steps included:

* Aligning game-level attendance with Caitlin Clark’s appearance data
* Converting inconsistent date formats across sources
* Engineering lagged player performance variables, including:
  * `Caitlin_points_lag3`
  * `Caitlin_minutes_lag3`
  * `Caitlin_3pts_made_lag3`
 
* Creating stadium-level historical features, such as:
  * `stadium_mean_prior_filled`
  * `stadium_rolling_k_mean_prior`
  * `stadium_prev_game_attendance`
  * `stadium_prior_games_count`

These features allowed the models to capture both short-term player effects and long-term venue trends.

---

## Modeling Approach

Three modeling strategies were evaluated:
* **Linear Regression**
  * Used as a baseline model for interpretability
  
* **Bagging**
  * Reduced variance and looked for overfitting
  
* **XGBoost**
  * Captured nonlinear relationships and feature interactions

Each model was evaluated before and after hyperparameter tuning using `GridSearchCV`, with performance measured using:

* R²
* Mean Squared Error (MSE)
* Root Mean Squared Error (RMSE)

---

## Results

* Untuned models performed poorly, with negative R² values for bagging and XGBoost
* After tuning, XGBoost emerged as the best-performing model:

  * R² ≈ 0.35
  * RMSE ≈ 2,609
* Linear regression and bagging improved after tuning but did not outperform XGBoost

---

## Model Interpretation

SHAP (SHapley Additive exPlanations) values revealed:
* `Caitlin_played` was the most influential predictor of attendance
* Stadium history features (`stadium_mean_prior_filled`, `stadium_prior_games_count`) were also highly important
* Visualizations showed consistently higher attendance when Clark played, across seasons, stadiums, and game types

---

## Key Takeaways

* Caitlin Clark’s presence has a statistically significant positive effect on WNBA attendance
* Model interpretability tools like SHAP are essential for understanding complex models
* Data engineering and feature construction were critical to achieving meaningful results

---

## Limitations

* Caitlin Clark has only played two WNBA seasons, limiting forecasting capability
* Clark's injuries in the WNBA reduced available observations
* Future schedules were unavailable, preventing forward-looking attendance predictions
* Even the best model achieved moderate (not high) predictive accuracy

---

## Future Work

* Expand analysis as Clark plays additional seasons
* Incorporate opponent strength and broadcast data
* Build true forecasting models once schedule data becomes available
* Apply similar frameworks to other high-impact athletes

---

## References

* WeHoop Library – WNBA Player and Game Data
* Across the Timeline – WNBA Attendance Data
* Journal of Applied Sport Management
* ESPN, NCAA, Associated Press reporting on WNBA attendance 

---
