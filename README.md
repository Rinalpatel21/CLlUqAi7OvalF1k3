# Happy Customer Project

## Project Description
This project analyzes and predicts customer happiness using the **ACME-HappinessSurvey2020** dataset. The objective is to identify the most influential factors driving customer satisfaction and to build predictive models that help businesses proactively improve customer experience and retention.

This end-to-end data science project covers:
- Exploratory Data Analysis (EDA)
- Data preprocessing and feature engineering
- Model development and tuning
- Model evaluation and comparison
- Business recommendations based on insights


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


# Exploratory Data Analysis (EDA)

EDA was performed to understand feature behavior and relationships with customer happiness.

### Key Steps:
- Checked for missing values and data consistency
- Analyzed feature distributions (histograms, boxplots)
- Reviewed class balance of target variable
- Generated correlation matrix and heatmaps
- Compared feature averages between happy vs unhappy customers

### Key Findings:
- Dataset slightly unbalanced between happy and unhappy customers
- Courier satisfaction (X5) and delivery timeliness (X1) showed positive relationship with happiness
- No severe multicollinearity observed among predictors

EDA helped guide model selection and interpretation strategy.


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
- Logistic regression performed well without heavy scaling due to similar feature ranges

### Train-Test Split
- Used stratified split to preserve class distribution
- Ensured reliable model evaluation

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

# Model Performance

Models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC
- Confusion Matrix

## Comparison of Model Effectiveness and Generalization

### Overfitting Tendencies
Many of the advanced models (Decision Tree untuned, Random Forest, Bagging, XGBoost, AdaBoost) exhibited significant overfitting. Their training performance was very high (e.g., F1-score > 0.8), but this dropped substantially on the test set (e.g., F1-score < 0.6). This indicates that these models learned the training data too well and failed to generalize to new, unseen data.

### Logistic Regression Models
The Logistic Regression models (both statsmodels and sklearn implementations) showed much better generalization. The difference between training and test set metrics was relatively small, suggesting they are not overfitting. Although their raw performance metrics (Accuracy, F1-score) are not as high as the overfit training scores of other models, their consistent performance makes them more reliable.

### Impact of X_mean Feature
The statsmodels Logistic Regression using only X_mean as a predictor achieved a remarkable recall of **0.905** on the test set. This highlights the potential simplicity in predicting happiness if an aggregate score is sufficiently informative. However, its precision is lower, meaning it might flag many customers as happy who are not.

### Optimal Threshold Application
Applying an optimal threshold (**0.45**) to the statsmodels Logistic Regression model (with all features) significantly boosted recall on the test set to **0.810**, while maintaining a reasonable F1-score of **0.680**. This demonstrates the importance of threshold tuning for specific optimization goals.

### sklearn Logistic Regression Performance
The sklearn Logistic Regression (with `class_weight='balanced'`) showed stable performance, with a test recall of **0.619**. Removing feature X6 from this model resulted in very similar performance (test recall **0.619**), suggesting X6 might not be a crucial predictor.

## Final Model Selection

Given the goal of maximizing Recall (to predict as many happy customers as possible to take action), the Logistic Regression model using only X_mean stands out with a test recall of **0.905**. While its precision (**0.633**) is not the highest, its ability to identify a large proportion of truly happy customers is superior. If the company prioritizes identifying most happy customers, even at the cost of some false positives, this model is the most effective.

Alternatively, Logistic Regression with all features and an optimal threshold of **0.45** also performed strongly with a test recall of **0.810** and a slightly better F1-score of **0.680**, offering a good balance.

**Conclusion:**  
Logistic Regression provided the optimal combination of predictive stability, explainability, and business relevance, making it the most suitable model for deployment in customer happiness prediction.

# Feature Importance Insights
### Most Important Features
Based on the statsmodels Logistic Regression (which offers interpretable coefficients), X5 (courier satisfaction) and X1 (on-time delivery) are the most important features positively impacting customer happiness. X3 (ordered everything wanted) and X4 (good price) are also significant. X2 ('contents as expected') is important, albeit negatively correlated, indicating it's still a significant factor in dissatisfaction.
### Minimal Set of Attributes
A minimal set of attributes that would preserve most information about customer happiness would likely include X1, X2, X3, X4, and X5. These features consistently show a positive and relatively strong association with customer happiness across models (especially logistic regression's odds ratios). X2 is important as it indicates a strong negative impact
### Question to Remove
X6 ('the app makes ordering easy for me') is the strongest candidate for removal in the next survey. Its impact on customer happiness, as measured by the odds ratio in logistic regression, is the smallest among all positive predictors (8% increase). More importantly, its removal from the sklearn Logistic Regression model resulted in virtually no change in performance metrics, indicating it provides minimal unique predictive value to this model.

### Important Business Consideration about Feature Elimination
Feature elimination does not imply that app usability is unimportant operationally. Rather, it indicates that within this dataset, app ease of ordering does not significantly differentiate happy and unhappy customers.


## Overall Insights and Actionable Recommendations
### Enhance Courier Experience
The courier interaction is the final brand touchpoint and has the biggest impact on satisfaction. Couriers should be trained in customer communication and professionalism, their performance should be tracked using customer ratings, high satisfaction scores should be incentivized, and best practices from top performers should be replicated. This approach leads to the fastest and largest improvement in customer happiness.

### Improve Delivery Reliability (X1)
On-time delivery builds trust and reliability. Delivery routes should be optimized using data, real-time tracking updates should be provided, customers should be notified proactively about delays, and courier capacity should be increased during peak hours. Implementing these actions reduces frustration and strengthens customer trust.

### Reduce Expectation Gaps (X2 — Risk Factor)
Customers become unhappy when orders do not match their expectations. Product descriptions and images should be improved, inventory should be synced in real time, order verification should be added before shipment, and customers should be notified early about substitutions. These measures result in fewer complaints and a smoother customer experience.

### Increase Data Collection
The small dataset size (126 rows) limits the effectiveness of complex models and their ability to generalize. Collecting significantly more customer feedback data is crucial for improving predictive accuracy and model robustness.

# Conclusions

- Key drivers of customer happiness were successfully identified.
- Logistic regression provided strong predictive power with interpretability.
- Small structured datasets may favor simpler models over complex ensembles.
- Predictive analytics can support proactive customer retention strategies.


