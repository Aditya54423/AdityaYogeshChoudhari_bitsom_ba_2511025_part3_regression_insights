# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary

A retail chain wants to understand what factors drive monthly sales performance across its stores. Leadership is considering actions like increasing marketing spend, improving inventory, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. Regression analysis was used to identify which factors are most strongly associated with monthly sales and to provide a data-backed recommendation.

---

## Dataset Description

- **File:** `business_regression_data.xlsx`
- **Records:** 320 store-month observations
- **Dependent variable:** `monthly_sales`
- **Numerical independent variables:** marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating
- **Categorical independent variables:** region (North/South/East/West), store_type (Mall/High Street/Residential/Airport)
- **Excluded from regression:** monthly_profit (too correlated with monthly_sales, r=0.69 — would cause data leakage)

---

## Dependent and Independent Variables

| Variable | Type | Role |
|---|---|---|
| monthly_sales | Numerical | Dependent (target) |
| footfall | Numerical | Independent — strongest predictor (R²=0.736 alone) |
| marketing_spend | Numerical | Independent — significant but modest (R²=0.167 alone) |
| inventory_availability_pct | Numerical | Independent — significant, high controllable impact |
| customer_rating | Numerical | Independent — significant (p=0.009) |
| staff_count | Numerical | Independent |
| holiday_flag | Binary (0/1) | Independent — significant (p=0.035) |
| avg_discount_pct | Numerical | Independent — NOT significant in either model |
| competitor_distance_km | Numerical | Independent — borderline |
| store_type | Categorical | Converted to 3 dummies (ref: Residential) |
| region | Categorical | Converted to 3 dummies (ref: East) |

---

## Regression Approach

Four models were built, all with `monthly_sales` as the dependent variable:

1. **Simple Regression 1 — Marketing Spend:** R² = 0.167
2. **Simple Regression 2 — Footfall:** R² = 0.736
3. **Simple Regression 3 — Avg Discount Pct:** R² = 0.008 (not significant)
4. **Multiple Regression — Final Model:** R² = 0.834

All regression outputs with coefficients, p-values, R-squared, and residuals are in `analysis/regression_workbook.xlsx`.

---

## Dummy Variable Approach

**store_type dummies created:**
- store_type_Mall, store_type_High Street, store_type_Airport
- **Reference category: Residential**

**region dummies created:**
- region_North, region_South, region_West
- **Reference category: East** (largest region — most stable baseline)

Full explanation with all coefficients in `outputs/model_equations.md`.

---

## Model Comparison Summary

| Model | R-squared | Adj R-sq | Key Finding |
|---|---|---|---|
| Simple — Marketing | 0.167 | 0.165 | Positive but weak |
| Simple — Footfall | 0.736 | 0.735 | Strongest single predictor |
| Simple — Discount | 0.008 | 0.005 | Not significant — discard |
| Multiple — Final | 0.834 | 0.828 | 10 of 12 variables significant |

---

## Final Model Selected

**Multiple Regression — R-squared = 0.834, Adjusted R-squared = 0.828**

**Equation:**
monthly_sales = 48,903 + 1.19×marketing_spend + 33.65×footfall − 47,714×avg_discount_pct + 3,060×inventory_availability_pct + 12,600×customer_rating + 13,911×holiday_flag + 6,379×region_North + 18,876×region_South + 19,294×region_West + 41,616×store_type_Airport + 18,404×store_type_High Street + 29,423×store_type_Mall

**Not significant:** avg_discount_pct (p=0.189), region_North (p=0.363)

---

## Business Recommendation

1. **Footfall is the dominant driver** — any strategy increasing store visits drives revenue (+₹33.65 per visitor)
2. **Airport format has the highest premium** — +₹41,616/month vs Residential, same inputs
3. **Inventory availability is the highest-ROI operational lever** — +₹3,060 per 1pp improvement
4. **South and West outperform East** — +₹18,876 and +₹19,294 respectively; North not significant
5. **Discounting does NOT drive sales** — not significant in any model, negative coefficient
6. **Pre-stock before holiday months** — +₹13,911 predictable seasonal lift

Full reasoning in `outputs/final_recommendation.md`.

---

## Residual Analysis Summary

- **Largest positive residual:** STR-1028 (Mall, East) — outperformed by +₹113,724
- **Largest negative residual:** STR-1017 (High Street, West) — underperformed by −₹172,039
- 3 of 5 worst underperformers are West-region stores — within-region variation exists beyond what a single dummy captures

Full analysis in `analysis/residual_analysis.md`.

---

## Assumptions and Limitations

- Association is not causation — coefficients show what moves together, not what causes what
- 16.6% of sales variation remains unexplained (store management quality, local conditions, etc.)
- Dataset covers one time window — relationships may differ across seasons or years
- Airport store sample is small (28 stores) — premium estimate carries more uncertainty
- region_North (p=0.363) should not drive North-specific investment decisions

---

## Screenshots Included

| File | Contents |
|---|---|
| `screenshots/simple_regression_output.png` | Simple regression output — footfall model |
| `screenshots/multiple_regression_output.png` | Multiple regression coefficients and R-squared |
| `screenshots/residuals_preview.png` | Top positive and negative residuals |
| `screenshots/model_comparison_preview.png` | Model comparison summary table |

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
