# 📄 Project Overview

This project focuses on developing a machine learning-based fraud detection system for credit card transactions.  
The goal was to accurately identify fraudulent activity while balancing detection performance with business impact.

Starting with raw transactional data, I built an end-to-end pipeline involving:

- **Data Cleaning:**  
  Handled missing merchant numbers and states, corrected ZIP code information using external data, and filtered transactions to retain only relevant records. Outliers (like extreme transaction amounts) were also addressed.

- **Feature Engineering:**  
  Created over 3,000 new variables capturing customer and merchant behaviors across multiple time windows (1, 3, 7, 14, 30, 60 days). Features included transaction counts, averages, maximums, variability measures, and geographical distance calculations.

- **Feature Selection:**  
  Used a two-stage approach:  
  - **Filter stage** based on Kolmogorov-Smirnov (KS) statistic to rank variables individually.  
  - **Wrapper stage** using sequential forward selection with a LightGBM model to select the best set of 20 multivariate features.

- **Model Building and Evaluation:**  
  Trained multiple machine learning models and manually cross-validated them using repeated random splits.  
  The best model, a LightGBM classifier, achieved a Fraud Detection Rate (FDR) of **~0.631** at a 3% investigation rate on out-of-time (OOT) data.

- **Business Impact Analysis:**  
  Developed savings curves showing fraud savings, false positive losses, and overall net savings across different score thresholds.  
  Estimated potential savings were calculated based on:  
  - A gain of $400 for each correctly identified fraudulent transaction  
  - A loss of $20 for each legitimate transaction incorrectly flagged  
  - Scaling the savings to 10 million transactions per year using the formula:

  > Estimated Savings = (12/2) × (10,000,000/100,000) × (Observed Savings on OOT Sample)

  Based on this, the model could save approximately **$51 million per year** if deployed at scale.

---

# 🛠 Tools and Libraries Used

- **Python** (main programming language)
- **Pandas, NumPy** for data wrangling
- **Scikit-learn, LightGBM, CatBoost, XGBoost, MLxtend** for modeling and feature selection
- **Matplotlib, Seaborn** for visualizations

---

# Key Outcomes

- Full fraud detection pipeline: from raw data → business-ready model
- Strong performance on unseen (OOT) data
- Focus on practical cost-benefit analysis, not just model accuracy
- End result: a deployable fraud detection system with large potential financial savings
