# MSCS-634 Project — Deliverable 3  
### Author: Sandesh Shrestha  
### Course: Data Mining & Analytics  

## Overview
This deliverable extends the analyses from previous project phases by applying multiple data mining techniques—including classification, hyperparameter tuning, clustering, and association rule mining—to the Walmart Sales dataset.  
The goal is to build predictive models, uncover natural groupings in sales behavior, and discover frequent patterns that provide actionable insights for retail decision-making.

---

## Dataset Description
The Walmart Sales dataset contains weekly sales records along with attributes such as temperature, fuel price, CPI, unemployment, store identifiers, and holiday indicators.

### Key preprocessing steps:
- Converted the **Date** column to datetime format.  
- Engineered **Year**, **Month**, and **WeekOfYear** for temporal analysis.  
- Created a binary classification target:  
  - **High_Sales = 1** if Weekly Sales ≥ median  
  - **High_Sales = 0** otherwise  
- Handled missing values and standardized numerical features for modeling.

---

## 1. Classification Models

Two supervised classification algorithms were implemented:

### **1. Decision Tree Classifier (Baseline)**
- A rule-based model that provides interpretability.  
- Demonstrated strong performance in predicting high vs. low weekly sales.  
- ROC and confusion matrix visualizations showed effective class separation with relatively few misclassifications.

### **2. K-Nearest Neighbors (KNN)**
- Provided smoother probability estimation and achieved one of the highest ROC-AUC scores.  
- Demonstrated excellent discrimination ability between the two classes.  
- Slightly more prone to false negatives, an important consideration in retail forecasting.

### Evaluation Metrics:
- Accuracy  
- Precision, Recall  
- F1-score  
- Confusion Matrix  
- ROC Curve and AUC  

Both models showed strong ability to predict sales outcomes based on historical and contextual features.

---

## 2. Hyperparameter Tuning

A Decision Tree classifier was optimized using **GridSearchCV** to explore parameters such as:

- `max_depth`  
- `min_samples_split`  
- `min_samples_leaf`  
- `criterion` (gini, entropy)

### Insights:
- Tuning improved model stability and reduced overfitting.  
- Best parameters were identified using cross-validation.  
- ROC-AUC and confusion matrix results were consistent with the baseline, indicating the model was already well-structured.

---

## 3. Clustering Analysis (K-Means)

Unsupervised learning was applied to identify natural groupings in weekly sales behavior.

### Steps:
- Selected features relating to sales, seasonality, and economic conditions.  
- Standardized numerical features using **StandardScaler**.  
- Computed **silhouette scores** for k = 2 through k = 6.  
- Identified optimal k based on peak silhouette value.  
- Visualized clusters using **PCA** for dimensionality reduction.

### Cluster Insights:
- Well-defined clusters revealed different sales behavior patterns.  
- High-sales clusters were strongly associated with holidays or seasonal periods.  
- Other clusters reflected lower or more stable weeks influenced by economic conditions.  

These clusters provide actionable insight for staffing, inventory management, and promotional planning.

---

## 4. Association Rule Mining (Apriori)

Boolean features were engineered to support association rule mining, such as:

- High vs. low temperature  
- Holiday flag  
- High vs. low CPI, fuel price, unemployment  
- Seasonal indicators  

Using the **Apriori** algorithm, rules were evaluated based on:

- Support  
- Confidence  
- Lift  

### Insights:
- Strongest rules showed that warm seasons, higher temperatures, or holiday conditions significantly increase the likelihood of high sales.  
- Lift values above 1.0 confirmed meaningful associations beyond random chance.  
- Economic indicators contributed to several high-lift rules, highlighting their influence on consumer behavior.

---

## 5. Visualizations

The notebook includes the following visualizations with corresponding interpretations:

### Classification:
- Confusion matrices  
- ROC curves  
- Model performance metrics  

### Clustering:
- Silhouette score plots  
- PCA scatterplot of clusters  
- Cluster profile summaries  

### Association Rules:
- Table of top rules  
- Bar chart of lift values for strongest rules  

All visualizations contain written interpretations explaining their significance and the insights gained.

---

## 6. Key Takeaways

- Machine learning models can reliably predict high-sales and low-sales weeks.  
- KNN demonstrated exceptionally strong ROC-AUC performance.  
- Hyperparameter tuning improved stability and reduced overfitting for the Decision Tree.  
- K-Means revealed meaningful segmentation of weekly sales patterns driven by seasonality, holidays, and economic trends.  
- Association rules uncovered key conditions that strongly increase the likelihood of high sales.  

Overall, these analyses provide deep and actionable insights into the factors driving weekly retail performance.

---

## 7. Challenges Encountered & How They Were Addressed

### **1. Noisy retail data affecting clustering quality**
Silhouette scores were relatively modest due to noise in economic/seasonal variables.  
**Solution:** Standardization + PCA visualization ensured cluster validity.

### **2. Choosing thresholds for discretizing continuous variables**
Binary features for association rule mining required careful threshold selection.  
**Solution:** Used median-based binning to ensure balanced support.

### **3. Balancing interpretability and performance in classification**
More complex models performed well but were less interpretable.  
**Solution:** Combined interpretable models (Decision Tree) with high-performing models (KNN).

### **4. Avoiding data leakage during preprocessing**
Preprocessing pipelines had to ensure no leakage into test data.  
**Solution:** Encapsulated all transformations inside `Pipeline` and `ColumnTransformer`.
