# Employee Turnover Prediction and Analysis

## Project Overview

This project analyzes employee data from Salifort Motors, a fictitious multinational vehicle manufacturing corporation, to understand the key drivers behind employee turnover and build a predictive model to identify employees at risk of leaving. High employee turnover is a significant concern for Salifort Motors due to its financial costs (recruiting, training) and impact on company culture.

The goal of this analysis is to provide data-driven insights and actionable recommendations to the Human Resources (HR) department to improve employee retention and job satisfaction.

## Data

The dataset used for this project is `HR_capstone_dataset.csv`. It contains 14,999 rows and 10 columns, representing self-reported information from employees.

**Data Dictionary:**

| Column Name             | Type      | Description                                                      |
| ----------------------- | --------- | ---------------------------------------------------------------- |
| `satisfaction_level`    | float64   | The employee’s self-reported satisfaction level \[0–1]           |
| `last_evaluation`       | float64   | Score of employee's last performance review \[0–1]              |
| `number_project`        | int64     | Number of projects employee contributes to                       |
| `average_monthly_hours` | int64     | Average number of hours employee worked per month              |
| `time_spend_company`    | int64     | How long the employee has been with the company (years)          |
| `work_accident`         | int64     | Whether or not the employee experienced an accident while at work |
| `left`                  | int64     | Whether or not the employee left the company (Target Variable: 1 if left, 0 if stayed) |
| `promotion_last_5years` | int64     | Whether or not the employee was promoted in the last 5 years     |
| `department`            | object    | The employee's department                                        |
| `salary`                | object    | The employee's salary (low, medium, or high)                    |

## Exploratory Data Analysis (EDA) Highlights

Key findings from the exploratory data analysis revealed several factors strongly associated with employee turnover:

* **Satisfaction Level:** Employees with very low satisfaction levels (below 0.4) were significantly more likely to leave.
* **Workload & Projects:** Employees working excessively high average monthly hours (e.g., over 240-250 hours) and those assigned a high number of projects (6 or 7 projects) showed a much higher propensity to leave, potentially indicating burnout.
* **Tenure:** Turnover was particularly high among employees with 3 to 5 years of tenure, often correlated with low satisfaction. A distinct group of employees with 7+ years also showed high turnover rates, which seemed less tied to low satisfaction but potentially related to other factors like compensation progression.
* **Promotion:** Receiving a promotion in the last 5 years was a strong indicator of an employee staying with the company. Employees who received a promotion were significantly less likely to leave, regardless of their hours worked.
* **Department:** While larger departments (Sales, Technical, Support) had the highest absolute numbers of leavers, some departments like HR and Accounting showed potentially higher proportions of turnover relative to their size.
* **Evaluation:** Employees with both very high hours and very high evaluation scores also showed a tendency to leave, suggesting potential burnout among high performers.

## Modeling

A Logistic Regression model was built to predict employee turnover (`left`).

**Data Preparation for Modeling:**

* Duplicate rows were removed.
* Categorical features (`department`, `salary`) were encoded into numerical formats (`department` using one-hot encoding, `salary` using ordinal encoding).
* Rows identified as outliers in the `time_spend_company` column (outside the IQR range of 1.5 to 5.5 years) were excluded for this specific model to potentially improve its performance and meet model assumptions.
* The data was split into training (75%) and testing (25%) sets, stratified by the target variable (`left`) to maintain class balance in both sets.

**Model Performance:**

The Logistic Regression model was evaluated on the test set using various metrics:

* **Overall Accuracy:** 82%
* **AUC Score:** 0.8037
* **Classification Report (for predicting 'left' - the minority class):**
    * **Precision:** 44%
    * **Recall:** 26%
    * **F1-score:** 33%

**Interpretation:**

The model demonstrates a good overall ability to distinguish between employees who will stay and those who will leave (indicated by the AUC score). However, its practical effectiveness in identifying employees who are actually at risk of leaving is limited. The low Recall (26%) means the model misses a large proportion of actual leavers, and the low Precision (44%) means that when it predicts someone will leave, it is often incorrect.

## Recommendations

Based on the analysis and model insights, the following recommendations are proposed to Salifort Motors HR:

* **Prioritize Employee Satisfaction Initiatives:** Implement targeted programs to understand and address the root causes of low satisfaction, especially among employees with scores below 0.4. Conduct deeper investigations (e.g., targeted surveys, focus groups) into the root causes of low satisfaction in different segments of the workforce.
* **Manage Workload & Prevent Burnout:** Review project assignments and average monthly hours, especially for employees with 6 or 7 projects and those consistently working very high hours. Explore strategies for better workload distribution and promoting work-life balance.
* **Review Compensation and Career Progression:** Evaluate salary and promotion structures, particularly for employees at key tenure milestones (3-5 years and 6+ years). Ensure competitive compensation and clear pathways for career growth to prevent stagnation-related turnover.
* **Implement Targeted Departmental Strategies:** Investigate the specific issues contributing to higher turnover in departments with high turnover (both in absolute numbers and rate) to address specific departmental challenges.
* **Utilize Predictive Analytics Proactively:** While the current model has limitations in identifying all leavers, the approach demonstrates the value of predictive analytics. Further development of the model (e.g., trying other algorithms, addressing class imbalance) or using its probability scores to flag potentially at-risk employees for early intervention discussions could be beneficial.

## Project Files

* Jupyter Notebook: (https://github.com/padman873/Course_7_Salifort_Motors_capstone_project/blob/main/Activity_%20Course%207%20Salifort%20Motors%20project%20lab.ipynb)
* PACE Strategy Document: (https://github.com/padman873/Course_7_Salifort_Motors_capstone_project/blob/main/Activity-Template_-Course-7-PACE-strategy-document.docx)
* Executive Summary: (https://github.com/padman873/Course_7_Salifort_Motors_capstone_project/blob/main/Activity-Templates_-Executive-summaries-Capstone.pptx)
* `HR_capstone_dataset.csv`: The dataset used for the project.

## How to Run the Code

1.  Clone this repository: `https://github.com/padman873/Course_7_Salifort_Motors_capstone_project`
2.  Navigate to the project directory.
3.  Ensure you have Python and Jupyter Notebook installed.
4.  Install necessary libraries (pandas, numpy, matplotlib, seaborn, scikit-learn): `pip install pandas numpy matplotlib seaborn scikit-learn`
5.  Open the Jupyter Notebook: `jupyter notebook capstone_project_notebook.ipynb`
6.  Run the cells in the notebook sequentially to reproduce the analysis and modeling steps.

## Ethical Considerations

Throughout this project, ethical considerations have been paramount, including ensuring data privacy, being mindful of potential biases in the data and model, transparently communicating model limitations, and emphasizing that the model's predictions should inform, not automate, HR decisions.

## Resources

* Pandas Documentation: https://pandas.pydata.org/docs/
* NumPy Documentation: https://numpy.org/doc/
* Matplotlib Documentation: https://matplotlib.org/stable/contents.html
* Seaborn Documentation: https://seaborn.pydata.org/api.html/
* Scikit-learn Documentation: https://scikit-learn.org/stable/documentation.html
* Stack Overflow: https://stackoverflow.com/
* Kaggle (Dataset Source): https://www.kaggle.com/
