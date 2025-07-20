# Retain the Legends: Using Game Data to Predict Player Churn 🎮


## Overview
This capstone project investigates player retention in *Apex Legends*, a popular free-to-play battle royale by Electronic Arts (EA). Using ranked match data, this project aims to predict player churn and identify key behavioral patterns that influence engagement. Insights are designed to support strategic decision-making for game designers, product managers, and monetization teams.

---

## Problem Statement
Live-service games like *Apex Legends* rely on sustained player engagement. High churn rates can negatively impact matchmaking, monetization, and community growth.  
> **Core Question:** *What in-game behaviors contribute to a player's likelihood to remain engaged or churn?*

---

## Project Objectives
- Build a machine learning model to classify players as retained or churned.
- Identify top behavioral features driving retention.
- Segment players into distinct behavioral groups using unsupervised learning.

---

## Dataset
- **Source:** [Kaggle - Apex Legends Season 15 Ranked Dataset](https://www.kaggle.com/)
- **Contents:** Raw match logs with timestamps, player IDs, kills, assists, placements, session durations, and more.

---

## Project Workflow 

### 1. Data Wrangling
- Cleaned missing values and duplicates.
- Parsed timestamps and engineered features:
  - `match_count_last_30_days`
  - `kill_death_ratio`
  - `legend_diversity_score`
  - `days_since_last_match`
  - `avg_session_duration`

### 2. Exploratory Data Analysis
- Visualized distributions, correlation heatmaps, and churn-related trends.
- Identified key patterns: players with low engagement variety and win rate had higher churn risk.

### 3. Modeling
- **Algorithms Tested:**
  - Logistic Regression
  - Random Forest
  - XGBoost (Best performer)
- **Results:**
  - **Accuracy:** `95%`
  - **F1 Score:** `0.91`
- SHAP used to explain top drivers of player churn.

### 4. Clustering (In Progress)
- Used K-Means clustering to group players by behavior:
  - Daily grinders
  - Casuals
  - Experimental players
- PCA applied for 2D visualization of player types.

---

## Tools & Technologies
- Python (Pandas, NumPy, Scikit-learn, XGBoost)
- SHAP (Explainability)
- Matplotlib & Seaborn (Visualization)
- Jupyter Notebook

---

## Key Features Used
- `kill_death_ratio`
- `session_frequency`
- `legend_switching_behavior`
- `ranked_to_casual_mode_ratio`
- `win_rate`
- `match_placement_consistency`

---

## Results Summary
- The **XGBoost model** delivered strong predictive performance.
- Feature importance insights:
  - Churn risk increases with long inactivity gaps, low K/D, and repetitive gameplay patterns.
- Results provide actionable insight for retention-based gameplay tuning.

