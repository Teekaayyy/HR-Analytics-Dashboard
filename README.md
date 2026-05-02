# Project 13: HR Analytics Dashboard
### Why Are Employees Leaving, and Who Is Most Likely to Leave Next?

---

## Business Brief

Employee attrition costs between 50% and 200% of an employee's annual salary when you factor in recruitment, onboarding, lost productivity, and institutional knowledge. Most HR teams track headcount and turnover rate. Very few use data to understand the drivers of attrition or predict who is at risk before they resign.

---

## Dataset

| Property | Detail |
|----------|--------|
| **Name** | IBM HR Analytics Employee Attrition Dataset |
| **Direct Link** | https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset |
| **Records** | 1,470 employees with 35 features |
| **Target** | Attrition: Yes / No |

---

## What Makes This Different

- Calculates the financial cost of attrition per department using industry benchmarks
- Assigns individual risk scores to every employee using a trained model
- Builds an Employee Risk Matrix: risk score vs seniority
- Identifies the Critical Risk segment: senior employees most likely to leave
- SQL-driven department and role analysis throughout

---

## Project Structure

```
hr-analytics-dashboard/
├── project_13_hr_analytics.ipynb
└── README.md
```

---

## Kaggle Setup

1. Search **"ibm-hr-analytics-attrition-dataset"** by *pavansubhasht* on Kaggle and attach it
2. Upload `project_13_hr_analytics.ipynb`
3. Run all cells

---

## Notebook Walkthrough

### Section 1: Setup
Libraries, colour system. Red = attrition/high risk, green = retained/low risk.

### Section 2: Load Data
Auto-detects CSV files. Tries multiple encodings.

### Section 3: Prepare Data
Standardises column names. Creates binary attrition column. Drops zero-variance columns (EmployeeCount, StandardHours, Over18 are always the same value in this dataset).

### Section 4: SQL HR Analytics Queries
Four SQL queries:
- Attrition rate by department with avg income, tenure, satisfaction
- Attrition rate by job role
- Attrition rate by overtime status
- Attrition rate by business travel frequency

### Section 5: Attrition Analysis Charts
Two chart panels:
- 6-panel categorical attrition rates (colour coded: red = above 1.3x average, amber = above average, green = below average)
- 6-panel numeric distributions comparing employees who left vs stayed (Age, MonthlyIncome, YearsAtCompany, DistanceFromHome, JobSatisfaction, WorkLifeBalance)

### Section 6: Financial Cost of Attrition
Assigns replacement cost multiplier by job level: 50% for L1, 100% for L2-L3, 150% for L4-L5. Calculates total and average cost per attrition event. Two charts: total cost by department and avg cost by job level.

### Section 7: Attrition Prediction Model
Label encodes all categorical features. Random Forest with class_weight=balanced (handles class imbalance). Evaluates on ROC-AUC and classification report. Feature importance horizontal bar chart and confusion matrix side by side.

### Section 8: Employee Risk Matrix
Scores every current employee with the trained model. Assigns risk tier (High >= 60, Mid 30-60, Low < 30). Interactive scatter: risk score vs job level, sized by monthly income. Shows high-risk threshold lines. Calculates critical risk count (high risk + L4/L5). Prints top 10 highest risk employees with department and role context.

### Section 9: Executive Summary Dashboard
Dark-theme KPI cards: total employees, attrition rate, model ROC-AUC, high-risk count, critical risk count, total estimated attrition cost.

### Section 10: Findings and Recommendations
Five findings with evidence. Four recommendations with specific actions.

---

## Key Findings

| Finding | Evidence |
|---------|----------|
| Attrition varies significantly by department and role | SQL analysis |
| Overtime is strongly associated with higher attrition | SQL overtime query |
| Income, overtime, and tenure are top predictors | Feature importance |
| A distinct critical risk population is identifiable | Risk Matrix |
| Attrition cost is concentrated in specific departments | Cost analysis |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | Data manipulation |
| SQLite3 | Department and role aggregation |
| Scikit-learn | Random Forest, LabelEncoder, StandardScaler |
| Plotly | Interactive Risk Matrix, dashboard |
| Matplotlib + Seaborn | Feature charts, confusion matrix |

---

*Built by Jessica Dan-Odhomo - [LinkedIn](https://www.linkedin.com/in/jessica-dan-odhomo) - [GitHub](https://github.com/Teekaayyy)*
