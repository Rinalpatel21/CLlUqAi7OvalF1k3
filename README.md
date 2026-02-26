# Happy Customer Project

## Project Description
This project analyzes and predicts customer happiness using the **ACME-HappinessSurvey2020** dataset. The objective is to identify the most influential factors driving customer satisfaction and to build predictive models that help businesses proactively improve customer experience and retention.

This end-to-end data science project covers:
- Exploratory Data Analysis (EDA)
- Data preprocessing and feature engineering
- Model development and tuning
- Model evaluation and comparison
- Business recommendations based on insights

---

# Dataset Overview

- Dataset: **ACME-HappinessSurvey2020.csv**
- Observations: 126 customer responses
- Features: 6 survey-based attributes
- Target Variable: Binary happiness indicator  
  - `1` = Happy  
  - `0` = Unhappy  

### Feature Descriptions (1–5 Rating Scale)

- **X1** – Order delivered on time  
- **X2** – Order contents as expected  
- **X3** – Ordered everything wanted  
- **X4** – Paid a good price  
- **X5** – Satisfaction with courier  
- **X6** – App ease of ordering  

All features are ordinal ratings, making the dataset structured and suitable for classification modeling.

---

# Exploratory Data Analysis (EDA)

EDA was performed to understand feature behavior and relationships with customer happiness.

### Key Steps:
- Checked for missing values and data consistency
- Analyzed feature distributions (histograms, boxplots)
- Reviewed class balance of target variable
- Generated correlation matrix and heatmaps
- Compared feature averages between happy vs unhappy customers

### Key Findings:
- Dataset slightly balanced between happy and unhappy customers
- Courier satisfaction (X5) and delivery timeliness (X1) showed strong positive relationship with happiness
- Pricing perception (X4) had weaker influence
- No severe multicollinearity observed among predictors

EDA helped guide model selection and interpretation strategy.

---

# Data Processing & Strategy

To ensure robust and unbiased modeling:

### Data Cleaning
- Verified no missing values
- Checked for outliers in rating scale (none outside 1–5 range)
- Confirmed consistent numeric formatting

### Feature Engineering
- Maintained ordinal structure of rating variables
- No categorical encoding required (already numeric)

### Scaling
- Applied standardization when required for certain models
- Logistic regression performed well without heavy scaling due to similar feature ranges

### Train-Test Split
- Used stratified split to preserve class distribution
- Ensured reliable model evaluation

---

# Model Approaches

A progressive modeling strategy was applied:

## Baseline Models
- Logistic Regression
- Decision Tree Classifier

Purpose:
- Establish benchmark performance
- Maintain model interpretability

## Advanced & Ensemble Models
- Random Forest
- Gradient Boosting
- Bagging Classifier

Purpose:
- Improve predictive performance
- Capture non-linear relationships

## Hyperparameter Tuning
- Used GridSearchCV
- Performed cross-validation
- Optimized:
  - Tree depth
  - Minimum samples per split
  - Class weights
  - Number of estimators

---

# Model Performance

Models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC
- Confusion Matrix

### Key Observations:
- Logistic Regression generalized well on test data
- Decision Trees showed risk of overfitting without tuning
- Ensemble methods did not significantly outperform logistic regression due to small dataset size
- Threshold optimization improved recall and business usability

### Final Model Selection:
**Logistic Regression** was selected due to:
- Strong generalization
- Interpretability
- Clear feature impact explanation
- Balanced precision-recall performance

---

# Feature Importance Insights

Odds ratio interpretation revealed:

- **X5 (Courier Satisfaction)** → Strongest positive driver of happiness  
- **X3 (Order Completeness)** → Significant positive impact  
- **X1 (On-Time Delivery)** → Meaningful contributor  
- **X4 (Pricing)** → Lower relative impact  

This insight helps prioritize operational improvements.

---

# Business Recommendations

Based on modeling and feature importance:

### Improve Courier Experience
- Invest in courier training and service quality
- Monitor delivery personnel ratings

### Ensure Order Accuracy
- Improve inventory management
- Reduce order fulfillment errors

### Maintain Delivery Timeliness
- Optimize logistics routing
- Monitor SLA adherence

### Implement Predictive Monitoring
- Use model probabilities to flag at-risk customers
- Proactively engage dissatisfied customers

---

# Conclusions

- Key drivers of customer happiness were successfully identified.
- Logistic regression provided strong predictive power with interpretability.
- Small structured datasets may favor simpler models over complex ensembles.
- Predictive analytics can support proactive customer retention strategies.

---

# Future Improvements

- Collect larger dataset for stronger model generalization
- Incorporate behavioral features (order frequency, complaints)
- Deploy model as API for real-time predictions
- Monitor model drift over time
- Conduct A/B testing on operational improvements

---

# Tech Stack

- Python
- Pandas
- NumPy
- Scikit-learn
- Statsmodels
- Matplotlib
- Seaborn

---


---
 This project demonstrates applied machine learning, statistical modeling, and business-focused analytics for customer experience optimization.
