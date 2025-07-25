# Retain the Legends: Predicting Player Churn in Apex Legends 🎮

## Overview
This project addresses the challenge of player retention in *Apex Legends*, EA’s flagship battle royale. Using detailed ranked match data, I built machine learning models to predict which players are likely to churn and to reveal in-game behaviors most closely tied to retention. Insights generated here provide strategic guidance for design, product, and live ops teams—helping keep the Apex Legends community thriving.


## Problem Statement
Player retention is critical for live-service games. High churn disrupts matchmaking, community growth, and monetization.
> **Main Question:** *What in-game behaviors most influence a player’s likelihood to churn or remain engaged, and how can we proactively predict churn?*


## Project Objectives
- Build a robust machine learning pipeline to classify players as retained or churned.
- Identify and interpret the top behavioral predictors of retention.
- Segment players into behavioral cohorts using unsupervised learning for more personalized engagement.


## Dataset
- **Source:** [Kaggle - Apex Legends Season 15 Ranked Dataset](https://www.kaggle.com/datasets/d8tary/apex-legends-season-15-ranked-dataset-raw)
- **Contents:** Match-by-match logs, player IDs, kills, assists, placements, session duration, and other engagement metrics.



## Workflow Summary

### 1. Data Wrangling & Feature Engineering
- Cleaned and validated raw data (duplicates, missing values).
- Parsed timestamps and engineered features:
    - `match_count_last_30_days`
    - `kill_death_ratio`
    - `legend_diversity_score`
    - `days_since_last_match`
    - `avg_session_duration`
- Ensured no data leakage with careful splits and SMOTE for class balance.

### 2. Exploratory Data Analysis
- Visualized class imbalance, feature relationships, and churn trends.
- Key patterns: players with low engagement variety, long inactivity, and poor match performance were most likely to churn.

### 3. Modeling & Evaluation
- **Algorithms tested:**
    - Logistic Regression (baseline)
    - Random Forest (ensemble, non-linear)
    - XGBoost (best performer)
- **Best Results (XGBoost):**
    - **Accuracy:** 91%
    - **F1 Score:** 0.84
- Used SHAP for feature importance and transparency.

### 4. Clustering & Segmentation (In Progress)
- K-Means clustering to group players by behavioral traits:
    - Daily Grinders
    - Casuals
    - Experimenters
- Used PCA for 2D visualization.


## Tools & Technologies
- **Python:** pandas, numpy, scikit-learn, XGBoost
- **Visualization:** matplotlib, seaborn
- **Explainability:** SHAP
- **Jupyter Notebook**


## Key Features Engineered
- `kill_death_ratio`
- `session_frequency`
- `legend_switching_behavior`
- `ranked_to_casual_mode_ratio`
- `win_rate`
- `match_placement_consistency`


## Results & Insights
- **XGBoost provided the best performance** on test data.
- **Top churn predictors:**
    - Long inactivity gaps
    - Low K/D ratio
    - Repetitive, low-variety play
- **Business value:**
    - Supports targeted player interventions and retention campaigns.
    - Informs game design and balance decisions with actionable data.


## Next Steps
- Finalize player segmentation and integrate findings into dashboards.
- Deploy churn prediction in EA’s live analytics pipeline.
- Retrain models with each new season to capture evolving meta/trends.


## Project Value
This project offers a practical, data-driven blueprint for increasing retention in live-service games.
**EA’s Apex Legends team can use these results to reduce churn, enhance engagement, and maximize player lifetime value—helping the game (and its community) continue to grow.**


