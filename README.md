# Background and Objectives

XYZ Company faces a high annual employee attrition rate of 16.1%. This effect negatively impacting project workflows, increasing recruitment costs, decreasing training efficiency, raising team workloads, and leading to a loss of key knowledge workers.

## Why This Matters

Employee attrition is a universal business challenge that directly affects productivity. The ideal attrition rate varies by industry, the general rate is around 10%. With a current gap of 6.1% from this ideal, a timely analysis is crucial to identify root causes and implement strategic solutions.

# Problem & Objective

## Problem
- 16.1% attrition per year from total employee in 2015
- normally attrition rate ranges between 5 to 10% per year
- estimated attrition cost around INR 263 Million Per Year

## Goals
- Reduce Attrition to 10% in 1 year
- Early Warning
- Workforce Planning
- Knowledge Management

## Objective
- Identify factors influencing employee attrition
- Build predictive models to detect employees at risk of leaving
- Determine the most influential factors as business intervention priorities
- Provide data-driven retention strategy recommendations

## Benefit
- Recruitment and training cost efficiency
- Increased operational stability

# Risk & Feasibility

## Risk

### Data Risk
- Irrelevant data
- Missing values
- Data imbalance

#### Mitigation
- Evaluation & adjustment
- Data cleaning & Processing
- Handling imbalance

### Model Risk
- Over/Underfitting
- Low interpretability

#### Mitigation
- Cross validation & Hyperparameter Tuning
- Use models that are easy to interpret

### Business Risk
- Result misinterpretation
- Stakeholder resistance
- Unactionable insight

#### Mitigation
- Clear visualization
- Early stakeholder involvement
- Focus on actionable insights

### Technical Risk
- Tools limitation
- Deployment failure
- Integration with HR systems

#### Mitigation
- Use simple tools
- Create a prototype
- Create a clear documentation

## Feasibility

### Technical Feasibility
- Available HR datasets.
- ML algorithms such as Logistic Regression and Random Forest are easy to use.
- Open-source tools that can be used and mastered by data scientist teams.

### Operational Feasibility
- Stakeholders can use the model results for retention strategies.
- Dashboards can help monitor attrition risk.

### Economic Feasibility
- Low costs due to the use of open-source tools.
- High benefits including reduced recruitment and training costs, and increased employee productivity.

# Data
- Source: Internal company data
- Scope: 4,410 employees
- Period: 2015 snapshot
- Format: Tabular HRIS export (.csv)
- Target Variable: Attrition (Yes/No)

## Dataset
- data_dictionary
- general_data
- manager_survey_data
- employee_survey_data
- in_time
- out_time

<img alt="Dataset ERD" src=https://github.com/raqiwardhana/FINPRO/blob/main/Asset/Dataset_Erd.png />

## Available Features

1. **Demographic & Personal**: Age, Gender, Marital Status, Education, Education Field, Distance from Home, Over18, NumCompaniesWorked
    
2. **Career Tenure & History**: TotalWorkingYears, YearsAtCompany, YearsSinceLastPromotion, YearsWithCurrManager, TrainingTimesLastYear
    
3. **Satisfaction Metrics**: JobSatisfaction, EnvironmentSatisfaction, WorkLifeBalance, JobInvolvement
    
4. **Job & Role Information**: Department, JobRole, JobLevel, BusinessTravel, EmployeeCount, EmployeeNumber, StandardHours
    
5. **Compensation & Benefits**: MonthlyIncome, PercentSalaryHike, PerformanceRating, StockOptionLevel
    
6. **Attendance**: in_time, out_time

# EDA
- Some data have positive skew distribution
<img alt="violin plot of EDA" src="https://github.com/raqiwardhana/FINPRO/blob/main/Asset/EDA_Violinplot.png" />

- On the Boxplot some data shown have outliers that need to be handled
<img alt="violin plot of EDA" src="https://github.com/raqiwardhana/FINPRO/blob/main/Asset/EDA_Boxplot.png" />

- Many of those who do attrition are:

    - Travel frequently
    - Human Resource as Education field
    - Human Resource Department
    - Job role as Research Director
    - Single
    - Overwork
    - Male
<img alt="Percentage of retention with bivariate" src="https://github.com/raqiwardhana/FINPRO/blob/main/Asset/EDA_percentage.png" />

- missing value:


|Column|Percentage|
| :--- | :--- |
|JobSatisfaction|(0.4%)|
|EnvironmentSatisfaction|(0.5%)|
|WorkLifeBalance |(0.8%)|
|NumCompaniesWorked |(0.4%)|
|TotalWorkingYears |(0.2%)|

- As per checking there is no duplicate data
identified in dataframes


# Preprocessing
- Outlier handled by using Log transformation ('MonthlyIncome', 'TotalWorkingYears', 'YearsAtCompany', 'YearsSinceLastPromotion', 'YearsWithCurrManager', 'overwork_days')
- missing value is handled by filled with the mode

# Feature Selection & Engineering
- drop data for having have constant value, StandardHours, EmployeeCount, Over18
- droping EmployeeID becasue irrelevant
- droping data with low correlation (e.g.'Gender', 'MonthlyIncome', 'NumCompaniesWorked', 'PercentSalaryHike, etc.')
<img alt="Percentage of retention with bivariate" src="https://github.com/raqiwardhana/FINPRO/blob/main/Asset/Future%20relation%20scale.png" />

# Modeling

## Preparation
- Split Data:

    - Train Data: 80%
    - Test Data: 20%

- Scaling: Standarixation
- Handling Imbalance: SMOTE
<img alt="Comparasion of before and after Attrition Distribution using SMOTE" src="https://github.com/raqiwardhana/FINPRO/blob/main/Asset/Attrition_Distribution_Compare.jpg"/>

## Baseline Model
- Using Logistis regression without the hyperparameter tuning for get the initial model performance

||Test|Train|
| :--- | :--- | :--- |
| Accuracy |0.85|0.86 |
| Precision |0.61| |
| Recall |0.24| |
| F1-Score |0.24| |
| ROC_AUC |0.77 |0.81 |
| Recall(CV) |0.24 |0.23 |

## Model Exploration

- Before tuning

| Model | Accuracy (Test) | Accuracy (Train) | Precision (Test) | Recall (Test) | F1-Score (Test) | ROC_AUC (Test) | Recall (Train) | Recall (CV Train) | Recall (CV Test) |
|-------|-----------------|------------------|------------------|---------------|-----------------|----------------|----------------|-------------------|------------------|
|Logistic_Regression|0.85|0.86|0.61|0.22|0.32|0.77|0.81|0.24|0.23|
|Decision_Tree|0.81|0.83|0.42|0.52|0.46|0.75|0.81|0.73|0.69|
|Random_Forest|0.95|0.99|0.92|0.75|0.83|0.97|1|0.96|0.91|
|XGBOost|0.99|1|1|0.96|0.98|0.99|1|1|0.99|

- After Tuning

| Model | Accuracy (Test) | Accuracy (Train) | Precision (Test) | Recall (Test) | F1-Score (Test) | ROC_AUC (Test) | Recall (Train) | Recall (CV Train) | Recall (CV Test) |
|-------|-----------------|------------------|------------------|---------------|-----------------|----------------|----------------|-------------------|------------------|
|Logistic_Regression|0.85|0.86|![up](https://img.shields.io/badge/0.62-brightgreen)|![up](https://img.shields.io/badge/0.23-brightgreen)|![up](https://img.shields.io/badge/0.33-brightgreen)|0.77|0.81|![down](https://img.shields.io/badge/0.23-red)|0.23|
|Decision_Tree|![up](https://img.shields.io/badge/0.92-brightgreen)|![up](https://img.shields.io/badge/0.97-brightgreen)|![up](https://img.shields.io/badge/0.76-brightgreen)|![up](https://img.shields.io/badge/0.7-brightgreen)|![up](https://img.shields.io/badge/0.73-brightgreen)|![up](https://img.shields.io/badge/0.91-brightgreen)|![up](https://img.shields.io/badge/0.98-brightgreen)|![up](https://img.shields.io/badge/0.81-brightgreen)|![up](https://img.shields.io/badge/0.74-brightgreen)|
|Random_Forest|![up](https://img.shields.io/badge/0.99-brightgreen)|![up](https://img.shields.io/badge/1-brightgreen)|![up](https://img.shields.io/badge/1-brightgreen)|![up](https://img.shields.io/badge/0.96-brightgreen)|![up](https://img.shields.io/badge/0.98-brightgreen)|![up](https://img.shields.io/badge/0.99-brightgreen)|1|![up](https://img.shields.io/badge/1-brightgreen)|![up](https://img.shields.io/badge/0.99-brightgreen)|
|XGBOost|0.99|1|1|0.96|0.98|0.99|1|1|0.99|

![up](https://img.shields.io/badge/Green-brightgreen) = Increasing
  
![down](https://img.shields.io/badge/Red-red) = Decreasing

==W=I=P==W=I=P==W=I=P==
