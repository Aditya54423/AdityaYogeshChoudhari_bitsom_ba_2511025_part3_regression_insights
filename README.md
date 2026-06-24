# Store Performance Regression Analysis

**Project:** Predicting Monthly Sales for Retail Stores  
**Dataset:** 80 stores × 4 months = 320 observations  
**Tools:** Excel (Data Analysis ToolPak)  


---

## Overview

This repository contains the complete regression workflow I developed for the store performance dataset. The objective was to identify which operational and locational factors drive monthly sales, and to quantify their relative importance.

I began with three simple regressions to establish baseline relationships, then built a full multiple regression model incorporating dummy variables for categorical factors (region and store type). The analysis covers data preparation, model estimation, comparison, residual diagnostics, and business recommendations.

---

## Key Findings

- **Footfall** is the dominant predictor, explaining 73.6% of sales variance in isolation and retaining a coefficient of **$33.65 per visitor** in the full model.
- **Marketing spend** has a positive but diminished effect in the multiple model: **$1.19 per $1 spent**, down from $2.13 in the simple regression, indicating that part of its apparent impact is attributable to correlated factors like footfall and store location.
- **Discount percentage** is not a statistically significant predictor of sales (p = 0.189) and carries a negative coefficient in both simple and multiple specifications.
- **Store type** exerts substantial influence. Airport stores outperform the Residential baseline by approximately **£41,616**, Mall stores by **£29,423**, and High Street stores by **£18,404**, holding all other variables constant.
- **Inventory availability** delivers a measurable return: each 1% improvement corresponds to roughly **£3,060** in additional monthly sales.

---

## Repository Structure

```
part3_regression_insights/
├── data/
│   └── business_regression_data.xlsx
├── analysis/
│   ├── regression_workbook.xlsx
│   ├── model_comparison.md
│   └── residual_analysis.md
├── outputs/
│   ├── regression_summary.xlsx
│   ├── final_recommendation.md
│   └── model_equations.md
├── screenshots/
│   ├── simple_regression_output.png
│   ├── multiple_regression_output.png
│   ├── residuals_preview.png
│   └── model_comparison_preview.png
└── README.md

```

---

## Data Notes

- The `month` column is stored as Excel serial dates. I excluded it from the regression because four time periods do not provide sufficient variation to model seasonality meaningfully, and treating serial dates as a continuous variable would be inappropriate.
- A small number of blank cells were present in `customer_rating` and `inventory_availability_pct`. Excel's Regression tool applies listwise deletion, so the final model is based on 320 complete observations.
- `staff_count` and `competitor_distance_km` were not included in the final model. The former is likely collinear with footfall and store type, and the latter contains extreme outliers that may violate linearity assumptions.

---

## Reproducing the Analysis

1. Enable the **Data Analysis ToolPak** in Excel.
2. Open `regression_workbook.xlsx`.
3. Use the `cleaned_data` sheet for simple regressions.
4. Use the `multiple_helper` sheet for the multiple regression, which contains the dependent variable and all predictors (including dummy variables) in a contiguous block.

---

