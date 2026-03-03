# Data Analysis Workflow Module

## Overview  
This project provides a **Python module** designed for a simple data analysis workflow, applicable to different data types.  
The workflow includes:  
1. **Data preprocessing** – handling missing values (imputation or drop) and automatic data type conversion  
2. **Statistical modeling** – explaining the effect of each variable on the target outcome  
3. **Model diagnostics and export** – residual checking and exporting results  

---

## Features  
- Load and preprocess CSV data into a custom `Data` object (a subclass of `pandas.DataFrame`)  
- Automatically handle missing values and data type transformation  
- Fit different statistical models depending on the response type:  
  - OLS regression for numerical response  
  - Logistic regression for binary categorical response  
  - Poisson / Negative Binomial GLM for count data  
- Diagnostic plots for model evaluation  
- Export model results (coefficients, odds ratios/rate ratios with confidence intervals) as `.csv`  

---

## Example Usage  

```python
import datloader as dl

# Load dataset
df = dl.Data('../data/CustomerTravel.csv', impute=False)

# Summarize variables
df.summary()

# Fit logistic regression model
mod1 = df.explain(response="Target", resp_type="categorical")

# Export results
mod1.out("model_result.csv")

# Fit logistic regression model
mod1 = df.explain(response="Target", resp_type="categorical")

# Export results
mod1.out("model_result.csv")
```

---

## Case Study
This project demonstrates its functionality using the Kaggle public dataset CustomerTravel.
A Logistic Regression model was applied to evaluate how explanatory variables influence the binary outcome: whether a user continues using the travel platform (Target = 0) or churns (Target = 1).
Key result:
After controlling for other factors, users who are frequent flyers (FrequentFlyer = Yes) have an odds ratio of 5.43 for churn compared to non-frequent flyers (FrequentFlyer = No).
This indicates that frequent flyers are about 5.4 times more likely to discontinue using the platform, suggesting that the most active travelers show a higher tendency to leave the service.
