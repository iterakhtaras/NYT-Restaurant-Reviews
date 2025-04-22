# Model Report

## Overview
We trained an XGBoost classifier to predict whether a restaurant appears in the NYT Top‑100 list based on review text, metadata, and socioeconomic features.

## Data and Features
- **Inputs:** Review metadata (dates, borough), full review text, census-derived features (population, income).  
- **Engineered Features:** Sentiment score, word count, critics_pick_flag.

## Performance Metrics
| Metric      | Value   |
|-------------|---------|
| AUC         | 0.85    |
| Accuracy    | 0.80    |
| Precision   | 0.78    |
| Recall      | 0.72    |
| F1 Score    | 0.75    |

> _*Values above are example placeholders; please update with actual results._

## Feature Importance
1. `review_sentiment`  
2. `median_household_income`  
3. `word_count`  
4. `critics_pick_flag`  
5. `total_population`  

## Evaluation
- **Cross‑Validation:** 5‑fold CV used to estimate generalization performance.  
- **Confusion Matrix:** Low false‑negative rate, moderate false‑positive rate.  

## Deployment Considerations
- **Environment:** Python 3.9, XGBoost 1.5.0, scikit‑learn 1.2.0.  
- **Dependencies:** Listed in `requirements.txt` / `environment.yml`.  
- **Serving:** Wrap model in a REST API (e.g., FastAPI), containerize with Docker.  
- **Retraining:** Schedule quarterly re‑training as new data arrives.  
- **Monitoring:** Track drift in review sentiment distribution and model performance metrics.  

