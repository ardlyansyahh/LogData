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

- Data that have consistent value are being drop ('Over18', 'EmployeeCount', 'StandardHours')
