# Model Comparison

## Models Built

Four regression models were run on this dataset — three simple and one multiple.

---

## Model 1: Simple Regression — Marketing Spend

- **Dependent variable:** monthly_sales
- **Independent variable:** marketing_spend
- **Intercept:** 560,777
- **Coefficient:** 2.13
- **R-squared:** 0.167
- **Adjusted R-squared:** 0.165
- **P-value (marketing_spend):** < 0.0001
- **Significant?** Yes

**Business usefulness:** Low on its own. Marketing spend explains only 16.7% of sales variation. The positive coefficient (each ₹1 in marketing = ₹2.13 in sales) is encouraging but the model leaves 83.3% of variation unexplained. Marketing contributes, but is not the primary driver.

**Limitation:** Ignores footfall, store type, region, and all operational variables. The coefficient likely overstates marketing's true standalone impact.

---

## Model 2: Simple Regression — Footfall

- **Dependent variable:** monthly_sales
- **Independent variable:** footfall
- **Intercept:** 446,411
- **Coefficient:** 35.68
- **R-squared:** 0.736
- **Adjusted R-squared:** 0.735
- **P-value (footfall):** < 0.0001
- **Significant?** Yes

**Business usefulness:** High. Footfall alone explains 73.6% of sales variation — stronger than any other single variable. Each additional visitor is associated with ₹35.68 more in monthly sales. This is the clearest single-variable signal in the dataset.

**Limitation:** Does not provide guidance on what levers to pull to increase footfall, and ignores store type, region, and operational variables.

---

## Model 3: Simple Regression — Avg Discount Pct

- **Dependent variable:** monthly_sales
- **Independent variable:** avg_discount_pct
- **Intercept:** 697,836
- **Coefficient:** -138,730
- **R-squared:** 0.008
- **Adjusted R-squared:** 0.005
- **P-value (avg_discount_pct):** 0.104
- **Significant?** No

**Business usefulness:** None. Discount percentage explains less than 1% of sales variation and is not statistically significant. The negative coefficient suggests higher discounts are weakly associated with lower sales — the opposite of what a "discounting drives sales" strategy would assume.

**Key finding:** Discounting should not be used as a lever to drive revenue. It shows no meaningful relationship with monthly sales in this dataset.

---

## Model 4: Multiple Regression — Full Model (Final Model)

- **Dependent variable:** monthly_sales
- **Independent variables:** marketing_spend, footfall, avg_discount_pct, inventory_availability_pct, customer_rating, holiday_flag + 6 dummy variables (region_North, region_South, region_West, store_type_Airport, store_type_High Street, store_type_Mall)
- **Reference categories:** region = East, store_type = Residential
- **R-squared:** 0.834
- **Adjusted R-squared:** 0.828
- **Standard Error:** 43,056
- **F-statistic p-value:** < 0.0001
- **Observations:** 320

**Significant variables (p < 0.05):**
- marketing_spend (p < 0.001)
- footfall (p < 0.001)
- inventory_availability_pct (p < 0.001)
- customer_rating (p = 0.009)
- holiday_flag (p = 0.035)
- region_South (p = 0.008)
- region_West (p = 0.002)
- store_type_Airport (p < 0.001)
- store_type_High Street (p = 0.002)
- store_type_Mall (p < 0.001)

**Not significant:**
- avg_discount_pct (p = 0.189) — consistent with Simple Model 3 finding
- region_North (p = 0.363) — North does not show a statistically meaningful difference from East
- Intercept (p = 0.308) — technically not significant but retained as a mathematical anchor

**Business usefulness:** Very High. Explains 83.4% of sales variation and covers all actionable levers: marketing, footfall, inventory, store format, and regional positioning.

---

## Summary Comparison Table

| Model | R-squared | Adj R-sq | Key Variables | Significant? | Recommended? |
|---|---|---|---|---|---|
| Simple 1 — Marketing | 0.167 | 0.165 | marketing_spend | Yes | Supplementary only |
| Simple 2 — Footfall | 0.736 | 0.735 | footfall | Yes | Baseline reference |
| Simple 3 — Discount | 0.008 | 0.005 | avg_discount_pct | No | Not useful |
| Multiple — Full Model | 0.834 | 0.828 | 10 of 12 significant | Mostly yes | YES — Final model |

---

## Which Model to Use

The multiple regression model is the recommended final model:

1. Highest R-squared (0.834) — best explanatory power
2. Covers variables leadership can directly act on (marketing, inventory, staffing, store type)
3. Isolates the contribution of each variable after controlling for the others

The simple footfall model (R² = 0.736) serves as a useful sanity check and communication tool for non-technical stakeholders. Simple Model 3 (discount) is important as a negative result — it explicitly rules out discounting as a useful sales lever.