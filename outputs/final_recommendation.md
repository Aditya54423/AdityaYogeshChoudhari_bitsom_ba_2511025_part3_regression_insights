# Final Recommendation — Monthly Sales Drivers

**For:** Retail Chain Leadership
**Based on:** Multiple regression analysis of 320 store-month records across 4 regions and 4 store formats
**Final model R-squared:** 0.834 (explains 83.4% of sales variation)

---

## Which Factors Are Most Strongly Associated with Monthly Sales?

### 1. Footfall — The Dominant Driver

- **Simple regression R-squared: 0.736** — footfall alone explains nearly 74% of sales variation
- **Multiple regression coefficient: +₹33.65 per visitor** (p < 0.001)
- No other single variable comes close to footfall's explanatory power
- Even after controlling for store type, region, marketing, and all other variables, footfall remains the single strongest predictor

**What this means:** More customers walking into the store = more sales. This is not surprising, but the regression quantifies just how dominant footfall is. Any strategy that increases store visits — better location, stronger marketing, improved in-store experience, anchor tenant partnerships — will likely drive revenue.

---

### 2. Store Format — Airport and Mall Premiums Are Real

After controlling for footfall, marketing, inventory, and region:

- **Airport stores:** +₹41,616/month vs Residential (p < 0.001) — the highest format premium
- **Mall stores:** +₹29,423/month vs Residential (p < 0.001)
- **High Street stores:** +₹18,404/month vs Residential (p = 0.002)
- **Residential stores:** Baseline (reference category)

**What this means:** Even with the same footfall, same marketing spend, and same inventory levels, an Airport store generates ~₹41,600 more per month than a Residential store. Format selection is a major strategic lever. When expanding, prioritise Airport and Mall locations over Residential formats.

---

### 3. Inventory Availability — Large Controllable Impact

- **Multiple regression coefficient: +₹3,060 per 1 percentage point** (p < 0.001)
- A store improving inventory availability from 80% to 90% (10 percentage points) is associated with approximately **₹30,600 more in monthly sales**
- This is nearly as large as the Mall format premium (₹29,423) and fully within operational control

**What this means:** Stockouts cost revenue. The data supports investing in better inventory management, replenishment processes, and supply chain reliability — these improvements have a directly measurable and statistically significant impact on sales.

---

### 4. Region — South and West Outperform East

After controlling for store format and all operational inputs:

- **West:** +₹19,294/month vs East (p = 0.002)
- **South:** +₹18,876/month vs East (p = 0.008)
- **North:** +₹6,379/month vs East — **NOT statistically significant (p = 0.363)**

**What this means:** South and West markets show a structural sales premium over East. North does not. When allocating expansion budget, South and West should be prioritised over North and East, assuming comparable store economics.

---

### 5. Marketing Spend — Positive but Modest

- **Simple regression coefficient: +₹2.13 per ₹1 spent** (R² = 0.167)
- **Multiple regression coefficient: +₹1.19 per ₹1 spent** (p < 0.001)
- The drop from ₹2.13 (simple) to ₹1.19 (multiple) shows that part of the simple model's effect was picking up the influence of other variables that correlate with marketing spend
- Positive return, but marketing explains only 16.7% of variation on its own

**What this means:** Marketing contributes, but is not the primary sales lever. Reallocating marketing budget from low-footfall, Residential-format locations to high-footfall, Airport/Mall locations is likely more effective than simply increasing total spend.

---

### 6. Customer Rating — Meaningful but Secondary

- **Multiple regression coefficient: +₹12,600 per 1-point rating increase** (p = 0.009)
- Statistically significant, but a smaller effect than inventory or store format

**What this means:** Better customer experience is associated with higher sales. Investment in service quality, staff training, and in-store experience has a measurable, positive association with revenue — though the mechanism (do high-rated stores attract more customers, or do more customers inflating ratings come from higher-traffic stores?) cannot be confirmed from this data alone.

---

### 7. Holiday Flag — Seasonal Opportunity

- **Coefficient: +₹13,911 in holiday months** (p = 0.035)
- A real, predictable seasonal effect

**What this means:** Holiday months deliver nearly ₹14,000 more in sales. Pre-loading inventory and staffing ahead of public holidays should be standard practice, not reactive.

---

## Variables That Should NOT Be Over-Interpreted

### avg_discount_pct — Do Not Use as a Sales Lever

- Simple regression R-squared: **0.008** — explains less than 1% of variation
- P-value: **0.104** (simple), **0.189** (multiple) — not statistically significant in either model
- Coefficient is negative in both models (more discounting weakly associated with lower sales)

**Leadership implication:** The data does not support increasing discounts to drive sales. Deeper discounting is likely to erode margins without generating meaningful revenue uplift. This is one of the clearest negative findings in the analysis.

### region_North — Cannot Conclude North Outperforms East

- Coefficient: +₹6,379, but p = 0.363 — not significant
- With the available data (64 North-region records), we cannot rule out that this apparent premium is due to sampling noise

**Leadership implication:** Do not make North-specific investment decisions based on this coefficient. Collect more data before drawing regional conclusions about North vs East.

### customer_rating — Direction Unclear

- Significant (p = 0.009) but the causality is ambiguous — high-revenue stores may receive higher ratings simply because they have better product availability and service capacity from higher investment, not because ratings themselves drive revenue.

---

## Business Actions Recommended (Priority Order)

1. **Audit inventory availability across all stores.** Identify stores in the bottom quartile of inventory_availability_pct and fix replenishment processes. The evidence shows a ₹3,060/month benefit per 1pp improvement — this is a high-ROI operational fix.

2. **Prioritise Airport and Mall formats in expansion planning.** The format premium is real and large (up to ₹41,616/month for Airport). When evaluating new locations, weight the store format premium explicitly in the business case.

3. **Focus expansion in South and West regions.** Both show statistically significant premiums over East (approximately ₹19,000/month). North does not show a significant difference from East at current sample sizes.

4. **Pre-position inventory and staff before holiday periods.** The ₹13,911 holiday lift is predictable. There is no reason to be caught understocked in these months.

5. **Treat footfall as the primary diagnostic metric.** When a store underperforms, check footfall first. If footfall matches peers but sales are lower, investigate inventory availability and customer experience. If footfall itself is low, investigate location and format.

6. **Stop seeking revenue through discounting.** The data provides no support for this strategy. Protect margins.

---

## Why Regression Shows Association, Not Causation

This is important for leadership to understand before acting on these results.

The regression model identifies variables that **move together** with monthly sales across 320 observations. It does not prove that changing one variable will cause a specific change in sales.

**Example:** The inventory coefficient (+₹3,060 per 1pp) means stores with higher inventory availability tend to have higher sales. But it is possible that high-revenue stores can afford better inventory management, rather than better inventory causing higher revenue. The direction of causality runs both ways.

**What this means for decisions:** Use the regression as a prioritisation tool — it identifies where to look and what to investigate further — not as a guaranteed return calculator. Before major capital allocation decisions (e.g., converting Residential stores to Mall format), validate the effect in a controlled test (A/B test, pilot store) rather than assuming the coefficient translates directly to the action.

---

## Risks and Limitations

- **16.6% of variation is unexplained.** Store management quality, local competition intensity beyond competitor_distance_km, lease terms, and store age are not in the dataset but likely matter.
- **One time window.** The data covers a single period. Seasonal patterns, economic conditions, and long-term trends are not captured.
- **Airport store sample is small (28 records).** The airport premium (₹41,616) is statistically significant but carries more uncertainty than the footfall or inventory coefficients.
- **Residual outliers need field investigation.** STR-1017 (High Street, West) underperformed by ₹172,039 and STR-1023 (Mall, South) underperformed by ₹142,688. No regression can diagnose what is operationally wrong with these specific stores — only a direct review can.
- **Customer rating causality is unclear.** The positive coefficient may reflect that high-revenue stores naturally deliver better experiences due to higher investment, not that improving ratings directly drives sales.
