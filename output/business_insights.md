# Business Insights Report
**Retail Executive Dashboard — FY 2024–2025**
*Prepared by: Bhoomi Solanki (2511412)*

---

## Calculated Fields Created in Tableau

| Calculated Field | Formula | Purpose |
|---|---|---|
| **Profit Margin** | `[Profit] / [Sales]` | Measures profitability efficiency per rupee of sales |
| **Cost** | `[Sales] - [Profit]` | Captures total cost of goods and operations |
| **Average Order Value** | `SUM([Sales]) / COUNTD([Order ID])` | Measures customer spending per transaction |
| **Return Rate** | `SUM([Return Flag]) / COUNT([Order ID])` | Measures product/service quality or fulfillment issues |
| **Shipping Delay Bucket** | `IF [Delivery Days] <= 1 THEN "Express (0-1d)" ELSEIF [Delivery Days] <= 3 THEN "Fast (2-3d)" ELSEIF [Delivery Days] <= 5 THEN "Standard (4-5d)" ELSEIF [Delivery Days] <= 7 THEN "Slow (6-7d)" ELSE "Very Slow (8+d)" END` | Categorizes delivery speed for actionable analysis |
| **Discount Band** | `IF [Discount] = 0 THEN "No Discount" ELSEIF [Discount] <= 0.10 THEN "Low (1-10%)" ELSEIF [Discount] <= 0.20 THEN "Medium (11-20%)" ELSEIF [Discount] <= 0.30 THEN "High (21-30%)" ELSE "Very High (31-35%)" END` | Groups discounts into business-relevant bands |
| **Profit vs Loss Flag** | `IF [Profit] > 0 THEN "Profitable" ELSE "Loss-Making" END` | Quick segmentation for loss detection |

---

## Business Insights

### Insight 1 — Sales Trend: Strong Overall Growth with Seasonal Peaks

**Observation:** Total sales over FY 2024–2025 reached approximately Rs 217 million, with consistent monthly performance. Peaks are visible in Q3 and Q4 of both years, suggesting seasonal demand spikes.

**Data Evidence:** Monthly trend analysis shows higher sales volumes in August–October and November–December periods across both 2024 and 2025.

**Business Interpretation:** Seasonal demand (festive, back-to-school, year-end budgets) is driving peak sales. This indicates predictable demand patterns that can be leveraged for supply and marketing planning.

**Recommended Action:** Pre-position inventory before peak months (Aug and Nov). Launch targeted promotions 2–3 weeks before peak periods. Align campaign budgets to Q3/Q4 heavy periods.

---

### Insight 2 — Regional Performance: South Leads, East Lags

**Observation:** South region generated the highest sales (Rs 64.7M) and profit (Rs 10.0M), while East region had the lowest sales (Rs 48.9M) and profit (Rs 7.6M).

**Data Evidence:**
- South: Rs 64.7M sales, Rs 10.0M profit
- North: Rs 54.6M sales, Rs 8.3M profit
- West: Rs 48.9M sales, Rs 7.4M profit
- East: Rs 48.9M sales, Rs 7.6M profit

**Business Interpretation:** South has outperformed due to a larger customer base or stronger market penetration. East's relatively lower performance despite comparable sales to West suggests lower profitability per transaction.

**Recommended Action:** Investigate East region for discounting practices, high return rates, or freight cost issues eroding margin. Consider targeted sales enablement programs for Eastern states.

---

### Insight 3 — Category Profitability: Technology Dominates, Furniture Underperforms Relatively

**Observation:** Technology accounts for 70%+ of total profit despite being approximately 70% of total sales. Furniture generates disproportionately lower profit margins compared to its sales volume.

**Data Evidence:**
- Technology: Rs 153.9M sales → Rs 28.0M profit (margin ~18.2%)
- Furniture: Rs 51.6M sales → Rs 3.6M profit (margin ~6.9%)
- Office Supplies: Rs 11.5M sales → Rs 1.7M profit (margin ~14.8%)

**Business Interpretation:** Furniture has high costs (possibly logistics, returns, damage) that compress margins. Technology products command better margins, potentially due to lower return rates and higher brand value.

**Recommended Action:** Review Furniture pricing strategy, reduce discounts on Furniture, and explore drop-shipping or third-party fulfillment to reduce logistics costs.

---

### Insight 4 — Sub-Category Profitability: Tables and Bookcases Are Margin Drains

**Observation:** Tables and Bookcases have the lowest absolute profit among all sub-categories, while Copiers, Accessories, and Phones are the top profit contributors.

**Data Evidence:**
- Tables: Rs 12.9M sales → Rs 731K profit (5.7% margin)
- Bookcases: Rs 12.5M sales → Rs 712K profit (5.7% margin)
- Copiers: Rs 40.6M sales → Rs 7.3M profit (18% margin)

**Business Interpretation:** Large-format furniture (Tables, Bookcases) likely has high shipping, assembly, and return costs. Technology accessories and copiers have higher inherent margins.

**Recommended Action:** Consider discontinuing or repricing low-margin Furniture sub-categories. Bundle Tables with accessories to increase per-order value. Prioritize Copiers and Accessories in marketing.

---

### Insight 5 — Customer Segment Behavior: Home Office Has Highest AOV

**Observation:** All three segments (Consumer, Corporate, Home Office) show near-equal total sales (~Rs 70–74M each), but Home Office customers show the highest average order values per transaction.

**Data Evidence:**
- Home Office: Rs 74.5M sales, Rs 11.6M profit (highest margin)
- Consumer: Rs 71.9M sales, Rs 11.0M profit
- Corporate: Rs 70.6M sales, Rs 10.7M profit

**Business Interpretation:** Home Office buyers tend to place fewer but higher-value orders. They likely purchase premium categories (Technology + Furniture together).

**Recommended Action:** Create Home Office bundles combining Furniture + Technology. Develop loyalty programs for Home Office segment to increase repeat purchase rate. Target Corporate segment with bulk-purchase discounts.

---

### Insight 6 — Discount Impact: Heavy Discounts Destroy Profitability

**Observation:** There is a moderate negative correlation (−0.27) between discount rate and profit. Orders with discounts above 20% show significantly reduced or negative profit.

**Data Evidence:** Scatter analysis shows that orders with discount = 0% have the highest profit per unit. At 31–35% discount bands, average profit turns near-zero or negative. Correlation coefficient = −0.27.

**Business Interpretation:** The current discounting strategy is eroding margin without proportionally increasing volume. High-discount orders in Furniture are particularly damaging.

**Recommended Action:** Cap discounts at 20% for all categories. Introduce value-added incentives (free shipping, bundled accessories) instead of direct price cuts. Review campaign channels that trigger heavy discounting.

---

### Insight 7 — Shipping Performance: Standard Class Has Highest Volume but Slowest Speed

**Observation:** Standard Class shipping handles the majority of orders (highest sales volume at Rs 122.8M) but averages 4.7 delivery days. Same Day shipping averages just 0.4 days.

**Data Evidence:**
- Same Day: 0.4 days avg | Rs 14.6M sales | Rs 2.2M profit
- First Class: 1.8 days avg | Rs 31.9M sales | Rs 4.6M profit
- Second Class: 2.7 days avg | Rs 47.7M sales | Rs 7.4M profit
- Standard Class: 4.7 days avg | Rs 122.8M sales | Rs 19.1M profit

**Business Interpretation:** Standard Class drives most of the business but could be a risk if customers become sensitive to delivery speed (especially post-COVID expectations). First Class offers a good speed-to-profit ratio.

**Recommended Action:** Offer free upgrade to First Class for high-value orders (>Rs 50K). Set SLAs for delivery performance and monitor delays by region. Use delivery speed as a promotional differentiator.

---

### Insight 8 — Return Pattern: Furniture Has Highest Return Rate

**Observation:** Furniture sub-categories account for 88 returns out of 191 total returns (46%), despite being ~24% of revenue. Office Supplies returns are 61 (32%) and Technology returns are 42 (22%).

**Data Evidence:**
- Furniture: 88 returns, ~5.7% return rate
- Office Supplies: 61 returns, ~3.9% return rate
- Technology: 42 returns, ~2.0% return rate
- Overall return rate: 4.55%

**Business Interpretation:** Furniture returns are likely driven by size/fit issues, damage in transit, or quality concerns. These returns add reverse logistics costs and reduce net margin further on an already low-margin category.

**Recommended Action:** Introduce 3D product visualization or size guides for Furniture online orders. Improve packaging quality for Tables and Bookcases. Implement a pre-shipping quality check to reduce damage-related returns.

---

### Insight 9 — Business Risk: Combined Impact of High Discounts + High Returns in Furniture

**Observation:** Furniture simultaneously has the highest return rate (46% of all returns), lowest profit margin (~6.9%), and is subject to discounting (average discount ~13–15% across orders). This triple exposure represents a concentrated business risk.

**Data Evidence:** Furniture margin of 6.9% combined with 5.7% return rate means effective margin after return costs could be close to breakeven or negative for some SKUs.

**Business Interpretation:** Any further increase in returns or discounting for Furniture could push it into loss-making territory at scale.

**Recommended Action:** Conduct a SKU-level profitability audit for all Furniture items. Prioritize phasing out or renegotiating supplier costs for Tables and Bookcases. Set a policy to cap Furniture discounts at 10%.

---

### Insight 10 — Business Opportunity: Technology + Organic/Referral Channel Synergy

**Observation:** Campaign channel analysis shows Organic and Referral channels drive high-quality, high-margin sales, particularly for Technology products.

**Data Evidence:** Technology contributes Rs 28M+ in profit. Organic and Referral channels tend to attract customers with genuine intent, which typically results in lower returns and higher satisfaction.

**Business Interpretation:** Customers acquired through organic search or referrals may have higher lifetime value (LTV) and lower acquisition cost than those from Paid campaigns.

**Recommended Action:** Increase SEO and referral program investment. Create a customer referral reward scheme for Technology purchases. Track LTV by campaign channel to confirm and optimize channel mix.
