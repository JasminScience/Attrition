
# Employee Attrition Analysis & Prediction

## Introduction

The goal of this project is to analyze and predict employee attrition (turnover) within an organization. Losing talented employees is costly for any business, so understanding the factors that lead to departures is crucial for effective human resource management.

In this study, I used a data-driven approach to:
1. **Analyze Key Drivers**: Identify why employees leave by examining variables such as income, work-life balance, and job roles.
2. **Data Visualization**: Create insightful visualizations to uncover hidden patterns in employee demographics and behavior.
3. **Predictive Modeling**: Build a Machine Learning model (Random Forest) capable of predicting whether an employee is likely to stay or leave the company.

By providing these insights, the project aims to help HR departments take proactive measures to improve employee retention and overall organizational stability.
# Age Analysis
•	The minimum age of employees who left the company is 18 years old
•	The maximum age is 58 years old
•	The average age of employees who left is 33.61 years — indicating that younger employees tend to leave more
# Gender
•	Male: 150 employees left
•	Female: 87 employees left
•	Males show a higher tendency to leave the company
# MaritalStatus
•	Single: 120 employees left (highest)
•	Married: 84 employees left
•	Divorced: 33 employees left (lowest)
•	Single employees are significantly more likely to leave
# Gender & Marital Status Combined
Gender	Marital Status	Total Left
Male	Single	          73
Male	Married	          53
Male	Divorced	      24
Female	Single	          47
Female	Married	          31
Female	Divorced	      9
# Advanced Analysis — Job Role, Education & Age Group
•	The group with the highest attrition: Male, Laboratory Technician, Education level 3, age 26-33 with 11 employees
•	The 26-33 age group dominates across most job roles
•	Laboratory Technician and Sales Executive are the most affected roles
# Years at Company vs Attrition
	     Avg Years at Company	Avg Years in Role	Avg Years Since Promotion	Avg Total Working Years
Stayed (No)	  7.37	                    4.48	            2.23	                  11.86
Left (Yes)	  5.13	                    2.90	            1.95	                   8.24
Employees who left had fewer years at the company, in their role, and in total working experience — suggesting that newer and less experienced employees are more likely to leave.
## Data Cleaning and Preparation

In this step, we ensure the data is high-quality and ready for modeling:
* **Missing Values**: Checked for null values using `.isnull().sum()` to ensure data completeness.
* **Statistical Summary**: Performed `.describe()` to understand the distribution and identify potential outliers.
* **Feature Removal**: Dropped 3 columns with constant values (zero variance), as they do not provide any predictive power for the model.
* **Data Integrity**: Verified the structure using `.info()` and handled any inconsistencies.

# 1. Exploratory Data Analysis (EDA)
To better understand the factors driving employee turnover, several visualizations were performed:
* **Attrition Distribution**: A Pie Chart was used to visualize the overall balance of the dataset (Stayed vs. Left).
* **Categorical Analysis**: Bar charts were created to compare Attrition across **Department**, **JobLevel**, and **Gender** to identify high-risk groups.
* **Age Distribution**: A Box Plot was used to analyze the age range of employees, showing that younger employees are more likely to leave.
* **Correlation Analysis**: A Heatmap of the correlation matrix was generated to identify strong relationships between numerical variables like Income, Years at Company, and Age.
# 3. Feature Engineering
In this stage, we transform the raw data into a format suitable for Machine Learning:
* **Categorical Encoding**: Applied  Attriton, OverTime, Gender
**One-Hot Encoding** (Dummy variables) to categorical features like `BusinessTravel`, `Department`,'EducationField' and `JobRole` and 'MaritalStatus' to convert text into numerical format.
# 4. Train-Test Split
To evaluate the model's performance on unseen data, we divided the dataset:
* **Target Variable (y)**: `Attrition`
* **Features (X)**: All other relevant columns after encoding.
* **Split Ratio**: 80% of the data was used for **Training** and 20% was reserved for **Testing** to validate the model's accuracy and generalizability.
* **Feature Scaling**: Used **StandardScaler** to normalize numerical variables (Age, MonthlyIncome, etc.). This ensures that features with larger scales do not dominate the model's learning process.
  # 5. Model Building: Random Forest Classifier
We selected the **Random Forest Classifier** due to its robustness and ability to handle complex relationships in tabular data:
* **Model Training**: The model was fitted using the scaled training data.
* **Performance Metrics**: We evaluated the model using an **Accuracy Score** and a **Classification Report** (Precision, Recall, and F1-Score).
* **Feature Importance**: Visualized the key drivers of attrition to provide actionable insights for the HR department.
# 6. Results Interpretation & Business Insights

### Model Performance Analysis
The **Random Forest** model achieved an overall accuracy of **87%**. However, the **Recall for the "Attrition" class (1)** is low (**0.10**). 
* **What this means:** While the model is very good at identifying employees who will stay, it currently struggles to catch those who are actually planning to leave. This is primarily due to the **class imbalance** (fewer "Yes" cases in the data).

### Key Drivers of Attrition (Feature Importance)
Based on our model's findings, the top factors contributing to employee turnover are:
1. **[Factor 1, e.g., MonthlyIncome]**: Lower salary levels show a strong correlation with higher attrition.
2. **[Factor 2, e.g., OverTime]**: Employees working frequent overtime are significantly more likely to leave.
3. **[Factor 3, e.g., Age/TotalWorkingYears]**: Junior employees or those in early career stages represent a higher risk group.

### Strategic Recommendations
* **Targeted Retention**: HR should focus on the top 10% of employees flagged by the model, even if the probability is low.
* **Work-Life Balance**: Reducing mandatory overtime could decrease turnover in high-risk departments.
* **Competitive Compensation**: Reviewing the pay scale for roles with high attrition importance is recommended.
# 7. Future Improvements (Addressing Low Recall)
While the model has high overall accuracy, the **Recall of 0.10** for the Attrition class indicates that the model is missing many employees who are likely to leave. To improve this in the future, I would:

* **Handle Class Imbalance**: Use techniques like **SMOTE** (Synthetic Minority Over-sampling Technique) to generate more examples of the minority class.
* **Adjust Class Weights**: Use the `class_weight='balanced'` parameter in Random Forest to penalize mistakes on the "Attrition" class more heavily.
* **Hyperparameter Tuning**: Use `GridSearchCV` to find the optimal settings for the model to better capture the minority class patterns.
