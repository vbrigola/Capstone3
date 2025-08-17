# Retain the Legends: Predicting Player Churn in Apex Legends (Season 15) 🎮

> I built an early-warning churn classifier for **Apex Legends – Season 15** that flags likely churners **one week early**. After fixing leakage, a **tuned Logistic Regression** gives the most reliable **recall** on the churn class—exactly what EA needs for pre-day-7 interventions.

## Problem
**Churn = 7 days of inactivity.** My goal is to predict churn **a week in advance** and identify the behaviors that move retention so Live Ops/design can intervene before players lapse.

## Data
- **Scope**: Ranked match logs from **Season 15** (placements, session timing, legend usage, combat stats).
- **Target**: Binary `churn` (1 if inactive ≥7 days).

## Pipeline (high level)
1. **Wrangling & Features**
   - Cleaned types/dupes; separated predictors `X` and label `y`.
   - **Cadence features**: `days_since_last_match`, `session_frequency` (7-day), `legend_diversity` (7-day), `match_duration`, `avg_kills`, plus `placement`.
   - **One-hots already present** for `map_*` and `legend_*`; `cat_cols = []` → no new dummies.
2. **Scaling & Split**
   - `StandardScaler` on numeric features.
   - **Stratified 80/20** split → `X_train` **(399 × 121)**, `X_test` **(100 × 121)**.
3. **Imbalance**
   - **SMOTE = diagnostics only** (previewed to 50/50 from `{0:283, 1:116}`); **training uses original distribution**.

## Modeling & Selection
- Tried: **Logistic Regression (baseline & tuned)**, **Random Forest**, **XGBoost**.
- **Selection rule**: maximize **F1 → PR AUC → ROC AUC** (recall-first policy for early warning).

### Test Metrics (S15)
| Model | Accuracy | F1 | Precision | Recall (churn) | PR AUC | ROC AUC |
|---|---:|---:|---:|---:|---:|---:|
| **Logistic Regression — tuned** | **0.37** | **0.47** | **0.31** | **0.97** | **0.304** | **0.516** |
| Random Forest — current | 0.55 | 0.24 | – | 0.24 | – | 0.413 |
| XGBoost — current | 0.62 | 0.27 | – | 0.24 | – | 0.492 |

**LR-tuned hyperparams**: `penalty='l1'`, `C=0.1`, `solver='liblinear'`, `max_iter=1000`, `random_state=42`.

## What actually drives retention
**Cadence > combat.** The strongest signals are **`days_since_last_match`**, **`session_frequency`**, **`legend_diversity`**, **`match_duration`** (with **`avg_kills`** secondary).

## What EA can do with this (actionable)
- **Day-5/6 nudges**: trigger outreach as `days_since_last_match` approaches 7.
- **Cadence goals**: simple, one-session tasks (e.g., “play 2 matches today,” “return tomorrow”).
- **Legend variety**: weekly “try 2 legends” prompts to lift `legend_diversity`.
- **Ranked placement micro-goals**: near-term placement targets to sustain momentum.

## Why recall-first
Missing a soon-to-churn player is expensive. I **prioritize recall** (catch ~**97%** of churners) and accept lower precision; EA can tune the operating threshold by campaign.

## Notebooks & data
- `2_PlayerRetention_DataWrangling.ipynb`
- `3_PlayerRetention_EDA.ipynb`
- `4_PlayerRetention_PreprocessingModeling.ipynb`
- `ApexPlayerRetention_final.csv`
- `FinalPresentation_ApexLegendsS15Churn.pdf`
- `FinalReport_ApexLegendsS15.pdf`

## Next steps
- Threshold/cost calibration (precision–recall trade-offs by campaign).
- Seasonal re-training and drift checks (apply to S16+).
- Live A/B tests using the risk score to measure lift in 7-day return.
