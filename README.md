# Credit Card Fraud Detection Model

## Project Overview
This project focuses on detecting fraudulent credit card transactions using machine learning models. Given the imbalance in fraud vs. normal transactions, I experimented with different approaches to achieve high fraud detection accuracy while minimizing false negatives. The core objective was to build a model that maximizes fraud detection without excessively misclassifying normal transactions as fraudulent.

## Dataset & Preprocessing
### Dataset Characteristics:
- Highly imbalanced, with fraudulent transactions significantly lower than normal transactions.
- Includes multiple transaction features for analysis.

### Initial Data Exploration:
- Checked for null values, missing data, class distribution, and balance ratio.
- Split data into features (X) and target (y), then into training and testing sets.

### Undersampling:
- Applied undersampling to balance the dataset for specific models like Logistic Regression.

## Modeling Approach
### Chosen Models & Why
- **Random Forest** – Excels in handling imbalanced data and offers high interpretability, making it valuable for fraud detection.
- **XGBoost** – Provides superior predictive power, and after fine-tuning, it significantly improved fraud detection sensitivity.
- **Logistic Regression (after undersampling)** – Performed best on the balanced dataset, making it a strong baseline for comparison.

### Fine-Tuning & Optimization
Hyperparameter tuning focused on multiple parameters to enhance model performance, including:
- **scale_pos_weight (XGBoost)** – Adjusted to ensure the model focuses more on fraud cases in the imbalanced dataset.
- **Threshold selection** – Fine-tuned to optimize fraud detection while managing false positives.
- **Other key parameters** – The number of estimators, maximum tree depth, and learning rate were optimized to improve model sensitivity, precision, and overall effectiveness.

Additional techniques applied:
- **Cost-Sensitive Learning** – Implemented to penalize the model more for misclassifying fraud cases as normal transactions.
- **Threshold adjustments** – Refined for both XGBoost and Random Forest, impacting their final performance.
- **Undersampling** – Applied to Logistic Regression, resulting in strong performance on balanced data.
- **Ensemble Learning** – Explored but did not outperform individual models, so it was not considered for future use.

## Evaluation Metrics & Performance
### Metrics Used:
- Precision, Recall, F1-score, ROC-AUC, and AUC-PR.

### Findings:
- Initially, Random Forest performed best.
- After fine-tuning, XGBoost outperformed Random Forest.
- However, after manual threshold adjustments, Random Forest regained top performance.
- Logistic Regression (after undersampling) performed the best among all models due to the balanced dataset.

## Final Model Decision (Real-World Banking Scenario)
The final model decision was based on fraud detection priority in a banking setting, where missing fraud is more costly than flagging false positives.

Two models were considered:

**Model A:**
- Detects all normal transactions correctly.
- Misses 3 fraudulent cases out of 50.

**Model B:**
- Misses only 2 fraudulent cases out of 50.
- Incorrectly flags a few normal transactions as fraud.

✅ **Final Decision:** Model B – The priority in banking is to reduce financial loss by minimizing undetected fraud, even if some normal transactions are mistakenly flagged.

## Challenges & Solutions
### Challenge 1: False Negatives (Fraud Cases Classified as Normal)
- **Problem:** XGBoost and Random Forest were correctly classifying normal transactions but struggled with false negatives.
- **Solution:**
  - Fine-tuned scale_pos_weight in XGBoost to focus more on fraud cases.
  - Adjusted threshold selection to improve recall without sacrificing too much precision.
  - Applied Cost-Sensitive Learning to penalize fraud misclassification.

### Challenge 2: Finding the Best Trade-off Between Fraud Detection & False Positives
- **Problem:** Increasing fraud detection caused an increase in normal transactions being misclassified as fraud.
- **Solution:**
  - Selected Model B, which captures more fraud cases while keeping false positives manageable.
  - Recognized that false positives can be manually reviewed in banking, whereas false negatives lead to financial loss.

## Future Enhancements
- **Model Deployment** – Implementing the model in a real-world banking system.
- **Further Feature Engineering** – Exploring additional transaction patterns and customer behavior features.

