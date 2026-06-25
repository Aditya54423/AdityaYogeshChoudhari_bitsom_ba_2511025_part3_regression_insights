# Model Equations

## Simple Regression Equations

### Model 1: Marketing Spend

**monthly_sales = 560,777 + 2.13 × marketing_spend**

- **Intercept (560,777):** Baseline expected monthly sales when marketing spend is zero. Treat as a mathematical anchor — no real store has zero marketing spend.
- **Coefficient (2.13):** Each additional ₹1 in marketing spend is associated with ₹2.13 in monthly sales.
- **R-squared: 0.167** — marketing spend alone explains 16.7% of sales variation.

---

### Model 2: Footfall

**monthly_sales = 446,411 + 35.68 × footfall**

- **Intercept (446,411):** Baseline expected sales at zero footfall.
- **Coefficient (35.68):** Each additional visitor is associated with ₹35.68 more in monthly sales.
- **R-squared: 0.736** — footfall alone explains 73.6% of sales variation. Strongest single predictor.

---

### Model 3: Avg Discount Pct

**monthly_sales = 697,836 − 138,730 × avg_discount_pct**

- **Intercept (697,836):** Baseline expected sales at zero discount.
- **Coefficient (−138,730):** Higher discount percentage is weakly associated with lower sales — but this coefficient is NOT statistically significant (p = 0.104).
- **R-squared: 0.008** — discount explains less than 1% of sales variation.
- **Conclusion:** This model has no business usefulness. Do not use discount as a sales lever.

---

## Multiple Regression Equation (Final Model)

**monthly_sales = 48,903 + 1.19 × marketing_spend + 33.65 × footfall − 47,714 × avg_discount_pct + 3,060 × inventory_availability_pct + 12,600 × customer_rating + 13,911 × holiday_flag + 6,379 × region_North + 18,876 × region_South + 19,294 × region_West + 41,616 × store_type_Airport + 18,404 × store_type_High Street + 29,423 × store_type_Mall**

---

## Explanation of Each Coefficient

| Variable | Coefficient | P-value | Significant? | Business Meaning |
|---|---|---|---|---|
| Intercept | 48,903 | 0.308 | No | Baseline: Residential store in East, all inputs at zero — mathematical anchor only |
| marketing_spend | 1.19 | <0.001 | Yes | Each ₹1 more in marketing → ~₹1.19 more in monthly sales |
| footfall | 33.65 | <0.001 | Yes | Each extra visitor → ~₹33.65 more in monthly sales |
| avg_discount_pct | −47,714 | 0.189 | No | Not significant — discounting does not meaningfully predict sales |
| inventory_availability_pct | 3,060 | <0.001 | Yes | Each 1pp improvement in inventory availability → ~₹3,060 more in monthly sales |
| customer_rating | 12,600 | 0.009 | Yes | Each 1-point increase in rating → ~₹12,600 more in monthly sales |
| holiday_flag | 13,911 | 0.035 | Yes | Holiday months generate ~₹13,911 more than non-holiday months |
| region_North | 6,379 | 0.363 | No | Not significant — North does not meaningfully differ from East |
| region_South | 18,876 | 0.008 | Yes | South stores generate ~₹18,876 more than East stores, same inputs |
| region_West | 19,294 | 0.002 | Yes | West stores generate ~₹19,294 more than East stores, same inputs |
| store_type_Airport | 41,616 | <0.001 | Yes | Airport stores generate ~₹41,616 more than Residential stores — largest format premium |
| store_type_High Street | 18,404 | 0.002 | Yes | High Street stores generate ~₹18,404 more than Residential stores |
| store_type_Mall | 29,423 | <0.001 | Yes | Mall stores generate ~₹29,423 more than Residential stores |

---

## Dummy Variable Approach

### Why dummy variables are needed

Store type and region are categorical — they have no natural numerical order. Assigning numbers (Mall=1, High Street=2, Residential=3) would imply a ranking that does not exist and would produce meaningless coefficients. Dummy variables convert each category into a 0/1 flag that the regression can handle correctly.

### Reference categories

| Categorical Variable | Reference Category | Why |
|---|---|---|
| region | East | Largest region by store count — provides the most stable baseline |
| store_type | Residential | Most common non-premium format — provides a neutral baseline |

Using a reference category avoids the dummy variable trap (perfect multicollinearity). If you include dummies for all 4 regions simultaneously, they perfectly predict each other and the regression becomes unsolvable. The solution is to drop one category — its effect is absorbed into the intercept, and all other coefficients are interpreted relative to it.

### How to read the dummy coefficients

- **store_type_Airport = 1** means "this store is an Airport store." The coefficient (+₹41,616) is the extra monthly sales an Airport store gets compared to an otherwise identical Residential store in the same region with the same footfall, marketing spend, inventory, and other inputs.
- **region_North = 1** means "this store is in the North region." The coefficient (+₹6,379) would mean North stores earn more than East stores — but since p = 0.363, this difference cannot be distinguished from random sampling variation. We cannot conclude North outperforms East.

---

## Final Model Selected

**Multiple Regression — Full Model**

**R-squared = 0.834 | Adjusted R-squared = 0.828 | N = 320**

### Why this model was selected

1. Highest R-squared (0.834) — explains 83.4% of monthly sales variation
2. Covers all actionable business levers leadership can influence: marketing spend, inventory availability, customer experience, store format selection, regional expansion priorities
3. Identifies which variables genuinely matter (10 of 12 significant at p < 0.05) and which do not (avg_discount_pct, region_North) — allowing leadership to focus attention on what the data actually supports
4. The improvement from Simple Model 2 (R² = 0.736) to this model (R² = 0.834) shows that variables beyond footfall carry real additional explanatory power

### Important caveat

All coefficients show association, not causation. The model cannot confirm that increasing inventory availability by 1 percentage point will produce exactly ₹3,060 in additional sales — only that stores with higher inventory availability tend to have higher sales, after controlling for the other variables. Business decisions should treat these coefficients as directional signals and order-of-magnitude estimates, not precise predictions.
