# bhoomisolanki_2511412_part4_tableau_dashboard

**Student:** Bhoomi Solanki
**Student ID:** 2511412
**Course Part:** Part 4 — Tableau Executive Dashboard & Data Storytelling

---

## Business Problem Summary

A retail leadership team needs an executive dashboard to monitor and evaluate:
- Sales performance and trends across time and regions
- Category and sub-category profitability
- Impact of discounts on profit margins
- Customer segment behaviour and purchasing patterns
- Shipping performance and delivery reliability
- Return patterns and associated business risk

The goal is to enable data-driven decisions that grow revenue, improve profitability, reduce return rates, and optimize discounting and logistics policies.

---

## Dataset Description

**File:** `data/dashboard_sales_data.xlsx`
**Sheet:** `dashboard_sales_data`
**Records:** 4,200 orders
**Date Range:** 1 January 2024 — 31 December 2025 (2 full fiscal years)

### Fields

| Column | Type | Description |
|---|---|---|
| order_id | String | Unique order identifier |
| order_date | Date | Date the order was placed |
| ship_date | Date | Date the order was shipped |
| customer_id | String | Unique customer identifier |
| customer_segment | Categorical | Consumer / Corporate / Home Office |
| region | Categorical | North / South / East / West |
| state | String | Indian state name |
| city | String | City name |
| category | Categorical | Furniture / Office Supplies / Technology |
| sub_category | Categorical | 13 sub-categories (Tables, Chairs, Copiers, etc.) |
| product_name | String | Individual product description |
| ship_mode | Categorical | Same Day / First Class / Second Class / Standard Class |
| sales | Float | Order sales value in Rs |
| quantity | Integer | Number of units ordered |
| discount | Float | Discount rate applied (0–0.35) |
| profit | Float | Net profit on order (can be negative) |
| return_flag | Binary | 1 = returned, 0 = not returned |
| delivery_days | Integer | Days between order date and ship date |
| customer_rating | Float | Customer satisfaction rating (2.1–5.0) |
| campaign_channel | Categorical | Organic / Social / Referral / Paid / Email / null |

### Assumptions

- Delivery days represent days between order_date and ship_date (pre-delivery processing time), not days from ship to arrival.
- Negative profit values represent loss-making orders (likely due to high discounts or return-related costs).
- Null values in campaign_channel (~32 records) are treated as "Unknown" channel.
- All monetary values are in Indian Rupees (Rs).
- Customer rating nulls (~32 records) are excluded from rating-based analysis.

---

## Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`

The packaged workbook contains:

### Sheets / Views

| Sheet Name | Purpose |
|---|---|
| Sales Trend | Line chart of monthly sales and profit from Jan 2024 to Dec 2025 |
| Regional Performance | Grouped bar chart comparing sales and profit by region; state-level top 10 bar |
| Category Profitability | Grouped bar (sales vs profit by category) + sub-category profit bar + margin % bar |
| Customer Segment View | Pie chart of sales by segment; grouped bar of profit by segment |
| Shipping Performance | Dual-axis bar: average delivery days and profit by ship mode |
| Discount vs Profit | Scatter plot of individual orders: discount rate vs profit |
| Return Analysis | Bar chart of return rate by category; heatmap of returns by segment × category |
| Executive Dashboard | Combined dashboard with all views, KPI cards, and filters |

---

## Calculated Fields Created

| Field Name | Formula | Purpose |
|---|---|---|
| Profit Margin | `[Profit] / [Sales]` | Measures profitability per rupee of sales |
| Cost | `[Sales] - [Profit]` | Total cost proxy (COGS + overhead) |
| Average Order Value | `SUM([Sales]) / COUNTD([Order ID])` | Average spend per unique order |
| Return Rate | `SUM([Return Flag]) / COUNT([Order ID])` | Proportion of orders returned |
| Shipping Delay Bucket | IF/ELSEIF on [Delivery Days]: 0-1=Express, 2-3=Fast, 4-5=Standard, 6-7=Slow, 8+=Very Slow | Categorizes delivery performance |
| Discount Band | IF/ELSEIF on [Discount]: 0=None, 0-10%=Low, 11-20%=Medium, 21-30%=High, 31-35%=Very High | Groups discounts for analysis |
| Profit vs Loss Flag | IF [Profit] > 0 THEN "Profitable" ELSE "Loss-Making" END | Quick classification for filtering |

---

## Dashboard Components

### KPI Cards (Top Row)
- **Total Sales** — Sum of all order sales values
- **Total Profit** — Sum of all order profits
- **Overall Profit Margin** — Profit / Sales as percentage
- **Overall Return Rate** — Returns as percentage of total orders

### Charts
1. Monthly Sales & Profit Trend (line chart)
2. Sales & Profit by Region (grouped horizontal bar)
3. Profit by Category (horizontal bar)
4. Sales by Customer Segment (pie chart)
5. Discount vs Profit (scatter plot)
6. Return Rate by Category (vertical bar)
7. Shipping Mode: Delivery Days vs Profit (dual-axis bar)
8. Profit by Sub-Category (horizontal bar, color-coded for positive/negative)
9. Returns by Segment × Category (heatmap)

---

## Filters and Interactions

### Dashboard Filters Applied
- **Region** — Filter all views by North / South / East / West
- **Category** — Filter by Furniture / Office Supplies / Technology
- **Customer Segment** — Filter by Consumer / Corporate / Home Office
- **Date Range** — Filter by order date (Jan 2024 – Dec 2025)
- **Ship Mode** — Filter by Same Day / First Class / Second Class / Standard Class
- **Campaign Channel** — Filter by Organic / Social / Referral / Paid / Email

### Action Interactions
- Clicking a Region bar filters the Category Profitability and Return Analysis views
- Clicking a Category bar highlights related sub-categories in the sub-category chart
- Scatter plot highlights update summary KPI values when discount bands are selected

---

## Key Business Insights

1. Technology drives 84%+ of total profit at 18.2% margin vs Furniture at 6.9%.
2. South region leads in sales (Rs 64.7M) and profit (Rs 10.0M); East is the lowest performer.
3. Tables and Bookcases are the worst-performing sub-categories with margins below 6%.
4. A discount rate above 20% consistently results in near-zero or negative profit.
5. Furniture has the highest return rate at ~5.7% — accounting for 46% of all returns.
6. Standard Class handles 60% of orders by value but averages 4.7-day delivery.
7. Home Office segment shows the highest profit absolute (Rs 11.6M) despite similar sales to peers.
8. Organic and Referral channels drive high-quality, lower-return-rate traffic.
9. Copiers and Accessories are the highest-margin sub-categories at ~18%.
10. Combined risk of high discount + high returns in Furniture makes it a structural threat to margin.

---

## Dashboard Story Summary

The retail business is healthy at the top line (Rs 217M sales, 15.3% overall margin) but faces concentrated structural risks in Furniture. Technology is the profit engine and should be prioritized in marketing. South and Home Office are the strongest geographic and segment opportunities respectively. The business must urgently cap discounts above 20%, address Furniture return rates, and invest in East region development. See `outputs/dashboard_story.md` for the full leadership narrative.

---

## Assumptions and Limitations

- No cost breakdown available (logistics, COGS, overhead are blended in the profit figure)
- Delivery days represents processing time, not transit time to customer
- Campaign channel nulls excluded from channel analysis
- Return flag is binary (no return reason captured) — limits root-cause analysis
- Two-year dataset limits long-term trend analysis and YoY benchmarking against prior periods
- Customer rating has ~32 null values, excluded from satisfaction analysis

---

## Screenshots Included

| File | Description |
|---|---|
| `screenshots/full_dashboard.png` | Complete executive dashboard with all views and KPI cards |
| `screenshots/sales_trend_view.png` | Monthly sales and profit trend line charts |
| `screenshots/regional_performance_view.png` | Regional and state-level performance bar charts |
| `screenshots/category_profitability_view.png` | Category and sub-category profitability analysis |
| `screenshots/filter_interaction_view.png` | Multiple filter views: Segment, Discount, Shipping, Returns, Channel, Delivery |

---

## Repository Structure

```
part4_tableau_dashboard/
├── data/
│   └── dashboard_sales_data.xlsx
├── tableau/
│   └── executive_dashboard.twbx
├── outputs/
│   ├── dashboard_story.md
│   ├── business_insights.md
│   └── chart_selection_justification.md
├── screenshots/
│   ├── full_dashboard.png
│   ├── sales_trend_view.png
│   ├── regional_performance_view.png
│   ├── category_profitability_view.png
│   └── filter_interaction_view.png
└── README.md
```
