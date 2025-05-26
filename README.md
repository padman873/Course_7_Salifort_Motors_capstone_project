# HR Analytics: Predicting Employee Turnover and Identifying Key Drivers

## 🚀 Project Overview

This project aims to analyze an HR dataset for "Salifort Motors" to understand the factors contributing to employee turnover. The primary goals are to identify key drivers of attrition, build a predictive model to identify employees likely to leave, and provide data-driven recommendations to help the HR department improve employee retention and reduce associated costs.

## 📊 Dataset

The dataset used contains information for approximately 15,000 employees (before cleaning) across 10 features, including:
* `satisfaction_level`: Employee-reported job satisfaction.
* `last_evaluation`: Score of the last performance review.
* `number_project`: Number of projects assigned.
* `average_monthly_hours`: Average hours worked per month.
* `tenure`: Years spent at the company.
* `work_accident`: Whether the employee had a work accident.
* `promotion_last_5years`: Whether the employee was promoted in the last 5 years.
* `department`: Employee's department.
* `salary`: Salary level (low, medium, high).
* `left`: Target variable indicating whether the employee left (1) or stayed (0).

## 🎯 Project Goals

1.  Perform comprehensive Exploratory Data Analysis (EDA) to uncover patterns and relationships related to employee turnover.
2.  Identify the key factors that significantly influence an employee's decision to leave the company.
3.  Develop a baseline predictive model (Logistic Regression) to classify employees as likely to leave or stay.
4.  Evaluate the model's performance, paying close attention to its ability to predict the minority class (employees who leave).
5.  Propose actionable, data-driven recommendations for the HR department to improve employee retention.

## 🛠️ Methodology & Workflow

1.  **Data Loading and Initial Inspection:** Loaded the dataset and performed initial checks for structure, data types, and missing values.
2.  **Data Cleaning:**
    * Standardized column names (e.g., to snake_case).
    * Identified and removed duplicate employee records (3,008 duplicates found and dropped).
3.  **Exploratory Data Analysis (EDA):**
    * Analyzed class balance for the target variable (`left`).
    * Conducted extensive univariate and bivariate analysis using visualizations (histograms, boxplots, scatterplots) to understand distributions and relationships between features and employee turnover.
    * Investigated correlations between numerical features.
4.  **Data Preprocessing for Modeling:**
    * Ordinally encoded the `salary` column (`low` < `medium` < `high`).
    * One-hot encoded the `department` column.
    * Filtered out outliers in the `tenure` column based on the IQR method (keeping tenures between 2-5 years for the logistic regression model, creating `df_logreg`).
5.  **Model Building (Baseline):**
    * Selected Logistic Regression as the initial model.
    * Split the preprocessed data (`df_logreg`) into training (75%) and testing (25%) sets, using stratification on the target variable.
    * Trained the Logistic Regression model on the training data.
6.  **Model Evaluation:**
    * Evaluated the model on the test set using a confusion matrix, classification report (precision, recall, F1-score), and AUC score.

## 💡 Key Findings & Insights

* **Major Drivers of Turnover:**
    * **Low job satisfaction** is strongly correlated with leaving.
    * **Excessive workload** (very high `average_monthly_hours` and/or high `number_project` - especially 6-7 projects) is a significant factor.
    * **Lack of recent promotion** (`promotion_last_5years` = 0) significantly increases the likelihood of leaving.
    * **Tenure:** Employees with longer tenure (particularly 5+ years, with very high attrition at 6-7 years) are more likely to leave. Analysis suggested that many long-tenured leavers were in lower salary brackets, indicating potential issues with compensation growth.
    * Distinct clusters of leavers were identified based on combinations of satisfaction, hours, and evaluation scores.
* **Departmental Impact:** While turnover occurs across all departments, larger departments like Sales, Technical, and Support show the highest absolute numbers of employees leaving.
* **Class Imbalance:** The data is imbalanced, with approximately 17% of employees in the cleaned modeling dataset (`df_logreg`) having left.

## ⚙️ Baseline Model Performance (Logistic Regression)

* **Overall Accuracy:** 82%
* **AUC Score:** 0.8827 (indicating good discriminative ability between classes)
* **Performance on "Left" Class (Minority Class):**
    * Precision: 0.44 (When the model predicts an employee will leave, it's correct 44% of the time)
    * Recall: 0.26 (The model identifies only 26% of employees who actually left)
    * F1-Score: 0.33
* **Conclusion:** While the model has decent overall accuracy and AUC, its ability to correctly identify employees who will actually leave (the primary goal for targeted intervention) is currently limited.

## 📈 Recommendations & Actionable Steps

Based on the EDA and baseline model results:

1.  **Enhance Employee Satisfaction:** Implement targeted programs to address low satisfaction, focusing on feedback mechanisms and improving the work environment.
2.  **Manage Workload:** Monitor and manage `average_monthly_hours` and `number_project` to prevent employee burnout, especially for high-performing individuals.
3.  **Review Compensation & Career Progression:** Re-evaluate salary structures and promotion opportunities, particularly for employees with longer tenure (5+ years), to ensure competitive compensation and clear career growth paths.
4.  **Department-Specific Strategies:** Investigate underlying reasons for higher leaver counts in key departments (Sales, Technical, Support) and develop tailored retention strategies.
5.  **Proactive HR Analytics:** Continue to invest in and leverage HR analytics to monitor trends, predict risks, and proactively address potential turnover drivers.

## 🛠️ Technologies & Libraries Used

* **Python 3**
* **Pandas:** For data manipulation and analysis.
* **NumPy:** For numerical computations.
* **Matplotlib & Seaborn:** For data visualization.
* **Scikit-learn:** For machine learning tasks (model building, splitting data, evaluation metrics).

## 🔮 Future Work & Model Improvements

* **Improve Minority Class Prediction:**
    * Apply techniques like `class_weight='balanced'` in logistic regression.
    * Experiment with resampling methods (e.g., SMOTE on training data).
* **Explore Advanced Models:** Build and evaluate other models identified as suitable (Decision Trees, Random Forest, XGBoost), which may better capture complex relationships and handle imbalance.
* **Hyperparameter Tuning:** Optimize chosen models for better performance.
* **Feature Engineering:** Explore creation of new features if deemed beneficial.
* **Deeper Dive:** Conduct further analysis on department-specific turnover reasons or the impact of manager effectiveness if data becomes available.

