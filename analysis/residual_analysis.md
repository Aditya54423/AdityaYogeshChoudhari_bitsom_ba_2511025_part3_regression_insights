## What Is a Residual

A residual is the difference between a store's actual monthly sales and what the model predicted:

**Residual = Actual Sales − Predicted Sales**

- **Positive residual:** Store outperformed what the model expected
- **Negative residual:** Store underperformed what the model expected

Large residuals are the most informative records — they represent stores the model cannot fully explain with the 12 variables included. Investigating them reveals what is missing from the model.

---

## Model Used

Multiple regression with 12 variables:
marketing_spend, footfall, avg_discount_pct, inventory_availability_pct, customer_rating, holiday_flag, region_North, region_South, region_West, store_type_Airport, store_type_High Street, store_type_Mall

Reference categories: region = East, store_type = Residential
R-squared = 0.834, Standard Error = ₹43,056

---

## Top 5 Largest Positive Residuals (Model Under-Predicted)

These stores performed significantly better than the model predicted.

| Store | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|
| STR-1028 | East | Mall | ₹713,611 | ₹599,887 | +₹113,724 |
| STR-1073 | East | Residential | ₹813,317 | ₹716,946 | +₹96,371 |
| STR-1050 | North | Residential | ₹735,787 | ₹642,886 | +₹92,900 |
| STR-1069 | West | High Street | ₹686,738 | ₹593,995 | +₹92,743 |
| STR-1030 | West | Residential | ₹820,519 | ₹729,696 | +₹90,823 |

### Business Interpretation

STR-1028 (Mall, East) outperformed by over ₹113,000 despite the model already accounting for its store type, region, footfall, and marketing. Something beyond the model's variables is driving this store's performance — possibly anchor tenant effects, proximity to a high-footfall event venue, or exceptionally strong store management. This store is worth studying to understand what drives its outperformance.

STR-1073 (Residential, East) outperformed by ₹96,371. Residential stores are the reference category — the lowest-expected format. A Residential store beating predictions by nearly ₹100,000 is a strong signal of either a micro-location advantage or a loyal local customer base not captured in any model variable.

STR-1050 (Residential, North) and STR-1069 (High Street, West) both outperform by ~₹92,000. The North dummy is not statistically significant, which makes STR-1050's outperformance particularly notable — this store is doing well despite operating in a region the model finds indistinguishable from East.

---

## Top 5 Largest Negative Residuals (Model Over-Predicted)

These stores performed significantly worse than the model predicted.

| Store | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|
| STR-1017 | West | High Street | ₹685,379 | ₹857,418 | −₹172,039 |
| STR-1023 | South | Mall | ₹627,172 | ₹769,860 | −₹142,688 |
| STR-1012 | West | Residential | ₹595,468 | ₹714,126 | −₹118,658 |
| STR-1007 | West | Mall | ₹800,452 | ₹909,679 | −₹109,227 |
| STR-1014 | West | High Street | ₹463,534 | ₹563,053 | −₹99,519 |

### Business Interpretation

STR-1017 (High Street, West) has the largest single residual in the entire dataset — the model expected ₹857,418 but it generated only ₹685,379, a shortfall of ₹172,039. The West region has a positive coefficient in the model (West stores tend to outperform East stores), making this store's underperformance even more striking — it is underperforming not just its prediction but its own regional peers.

Three of the five worst underperformers are in the West region (STR-1017, STR-1012, STR-1007). Despite the model awarding a positive West premium (region_West coefficient = +19,294), these specific stores are consistently below expectations. This suggests there is meaningful within-region variation in the West that a single regional dummy cannot capture — possibly local competition, lease-term constraints, or store-level execution issues.

STR-1023 (Mall, South) underperforms by ₹142,688 despite being in both a positive store-type (Mall) and a positive region (South). This is a high-expectation profile that is seriously underdelivering. This store should be a priority for operational review.

STR-1014 (High Street, West) has the lowest actual sales among the five worst residuals (₹463,534), which is well below the dataset average.

---

## Does the Model Systematically Bias Toward Any Group?

**West region:** 3 of the 5 worst underperformers are West stores. The West dummy is positive, meaning the model systematically expects West stores to outperform East — but a meaningful subset of West stores are not living up to that expectation. The model may be over-rewarding the West region.

**Mall stores:** Appear in both top positive (STR-1028) and top negative (STR-1023, STR-1007) residuals. Mall performance is highly variable — some Malls significantly outperform, others significantly underperform. A single Mall dummy does not fully capture this variation.

**No systematic bias against small/large stores:** The residuals are spread across different actual sales levels and footfall ranges, suggesting the model's errors are store-specific rather than scale-dependent.

---

## Limitations of This Residual Analysis

- Residuals represent one time window. A store with a large negative residual this period may have experienced a temporary disruption (construction, supply issue, staff turnover) rather than a structural problem.
- The model's standard error is ₹43,056, meaning residuals below ±₹43,000 are within expected model noise — only residuals significantly beyond this threshold are truly noteworthy.
- Identifying residual patterns is not the same as diagnosing root causes. Field investigation is required to understand why specific stores diverge from predictions.