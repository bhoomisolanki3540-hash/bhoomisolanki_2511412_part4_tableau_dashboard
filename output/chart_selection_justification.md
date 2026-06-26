# Chart Selection Justification
**Executive Dashboard — FY 2024–2025**
*Bhoomi Solanki (2511412)*

---

## Overview

Every chart in the executive dashboard was selected to answer a specific business question as clearly and efficiently as possible. This document explains the rationale behind each visualization choice, the design principles applied, and the pitfalls avoided.

---

## Chart 1: Line Chart — Monthly Sales & Profit Trend

**Business Question:** How are monthly sales and profit changing over time across FY 2024–2025?

**Why This Chart Type:**
Line charts are the standard for time-series data because they visually encode change over continuous time intervals. The human eye naturally follows lines and perceives slopes, dips, and peaks. For monthly aggregated data spanning 24 months, a line chart shows seasonality and trend simultaneously.

**Fields Used:**
- X-axis: Order Date (aggregated to Month/Year)
- Y-axis: SUM(Sales) / SUM(Profit) in Rs Millions
- Color: Two separate lines — Blue for Sales, Green for Profit
- Fill area (below lines) at 10% opacity for visual depth

**Design Principle Applied:** Dual encoding — both line position and fill area reinforce the magnitude. Limiting the chart to two lines avoids clutter while still communicating the relationship between sales and profit.

**Mistake Avoided:** Did not use a bar chart for this time series, which would have made trend comparison much harder to read across 24 bars side by side. Did not use a pie chart (inappropriate for time series). Avoided dual y-axis where the scales would be misleading — instead used two side-by-side trend lines with consistent axis units.

---

## Chart 2: Horizontal Bar Chart — Sales & Profit by Region

**Business Question:** Which region is performing best in absolute sales and profit terms?

**Why This Chart Type:**
Horizontal bar charts are ideal for categorical comparisons with clear magnitude differences. With only 4 regions, a grouped horizontal bar allows side-by-side comparison of Sales and Profit per region without clutter. Horizontal orientation accommodates label readability.

**Fields Used:**
- Y-axis: Region (categorical)
- X-axis: SUM(Sales) and SUM(Profit) in Rs Millions
- Color: Blue for Sales, Green for Profit (consistent palette across dashboard)
- Sorted: Ascending by Sales for easy top/bottom identification

**Design Principle Applied:** Consistent color encoding. Blue = Sales and Green = Profit is maintained across all charts in the dashboard so the viewer doesn't have to re-learn the color scheme on each chart.

**Mistake Avoided:** Did not use a map as the primary regional view (insufficient state-level granularity needed for this summary). Did not use a 3D bar chart, which would distort height comparisons.

---

## Chart 3: Grouped Bar Chart — Category Sales vs Profit with Margin Labels

**Business Question:** Which product categories are most profitable, and is sales volume correlated with profitability?

**Why This Chart Type:**
A grouped bar chart lets viewers compare two measures (Sales and Profit) side-by-side across categories. Adding margin percentage annotations directly on the Profit bar provides a third dimension of insight without adding a new visual element.

**Fields Used:**
- X-axis: Category (Furniture, Office Supplies, Technology)
- Y-axis: Rs Millions
- Left bar: SUM(Sales) at 70% opacity
- Right bar: SUM(Profit) at full opacity
- Color: Consistent category colors (Orange = Furniture, Blue = Office Supplies, Green = Technology)
- Label: Profit Margin % displayed above each Profit bar

**Design Principle Applied:** Annotation instead of a third bar — placing the margin % as a text label reduces the chart elements needed and answers three questions in one view.

**Mistake Avoided:** Did not use a pie chart to show category contribution, which would hide the absolute magnitude difference between Technology and others. Avoided stacked bars, which would have made individual segment comparison more difficult.

---

## Chart 4: Horizontal Bar Chart — Profit by Sub-Category (Color-Coded Positive/Negative)

**Business Question:** Which sub-categories are most and least profitable?

**Why This Chart Type:**
A horizontal bar chart sorted by profit value allows instant ranking. Using red for negative profit and green for positive profit provides immediate visual signal of sub-categories that are generating losses versus profit.

**Fields Used:**
- Y-axis: Sub-Category (sorted ascending by profit)
- X-axis: SUM(Profit) in Rs Millions
- Color: Red = negative profit (loss-making), Green = positive profit
- Reference line: Vertical line at 0 to anchor the loss/profit boundary

**Design Principle Applied:** Diverging color encoding — the semantic meaning of red (danger/loss) and green (success/profit) leverages pre-existing mental models without requiring a legend explanation.

**Mistake Avoided:** Did not sort alphabetically (which would have hidden the ranking story). Avoided using a treemap here because treemaps cannot clearly represent negative values.

---

## Chart 5: Scatter Plot — Discount vs Profit

**Business Question:** Is there a relationship between discount rate and profit? Do high discounts destroy margin?

**Why This Chart Type:**
Scatter plots are specifically designed to show correlation between two continuous variables. Each data point represents an individual order, allowing the viewer to see the distribution, density, and trend simultaneously. A horizontal reference line at y=0 immediately identifies orders that turned into losses.

**Fields Used:**
- X-axis: Discount (continuous, 0 to 0.35)
- Y-axis: Profit per order in Rs 000s
- Color: Encoded by Sales amount (darker blue = higher sales)
- Size: Fixed small size (15px) to avoid overplotting while maintaining density visibility
- Reference line: Horizontal dashed red line at Profit = 0

**Design Principle Applied:** Transparency (alpha=0.3) to handle overplotting — with 4,200 data points, overlapping dots would create a solid blob without transparency. The reference line creates a visual split between profitable and loss-making orders.

**Mistake Avoided:** Did not use a bar chart (which would aggregate and hide individual-order variation). Did not connect dots with a line (which would imply a time sequence that doesn't exist here). Avoided making dots too large, which causes severe overplotting.

---

## Chart 6: Bar Chart — Return Rate by Category

**Business Question:** Which product category has the highest return rate?

**Why This Chart Type:**
A simple vertical bar chart with three bars (one per category) provides instant comparison of return rates. The percentage label above each bar eliminates the need for viewers to read off the y-axis precisely.

**Fields Used:**
- X-axis: Category
- Y-axis: Return Rate (%) = SUM(Return Flag) / COUNT(Order ID) × 100
- Color: Consistent category colors (Orange, Blue, Green)
- Label: Return rate % above each bar

**Design Principle Applied:** Fewer is more — with only 3 categories, this chart is deliberately simple. Complexity would add no value. Labels directly on bars eliminate the need for a y-axis gridline read.

**Mistake Avoided:** Did not show raw return counts (absolute numbers) instead of rate, which would have been misleading since categories have different sales volumes. Did not use a pie chart to show return share, as that would misrepresent the story (we want to show rate, not composition).

---

## Chart 7: Dual-Axis Bar Chart — Shipping Mode: Delivery Days vs Profit

**Business Question:** How does shipping mode affect delivery speed and profitability?

**Why This Chart Type:**
A dual-axis bar chart allows comparison of two different-scale metrics (delivery days and profit in Rs millions) across the same categorical variable (ship mode). Using bars for both metrics at different scales requires visual distinction — here achieved through color (orange for delivery days, green for profit) and placement (left vs right within group).

**Fields Used:**
- X-axis: Ship Mode
- Left Y-axis: Average Delivery Days (orange bars)
- Right Y-axis: SUM(Profit) in Rs Millions (green bars)
- Color: Orange = delivery speed, Green = profit (intuitive separation)
- Legend: Clearly labelled to avoid dual-axis confusion

**Design Principle Applied:** Dual-axis charts are generally discouraged, but here both metrics share the same categorical dimension and neither is a ratio of the other — so the design is appropriate. Colors and legends prevent misinterpretation.

**Mistake Avoided:** Did not use a line on the second axis (which would imply a trend/time relationship that doesn't exist). Did not use identical colors for both bars, which would have created dangerous confusion with the dual y-axes.

---

## Chart 8: Pie Chart — Sales by Customer Segment

**Business Question:** What share of total sales does each customer segment represent?

**Why This Chart Type:**
Pie charts are appropriate when: (1) showing part-to-whole composition, (2) there are 3–5 segments only, and (3) differences in share are meaningful to the business. All three conditions are met here. The pie immediately communicates that no single segment dominates — all three hold roughly equal shares.

**Fields Used:**
- Slices: Customer Segment (Consumer, Corporate, Home Office)
- Size: SUM(Sales) per segment
- Color: Purple (Consumer), Blue (Corporate), Green (Home Office)
- Label: Segment name + percentage

**Design Principle Applied:** Used percentage labels, not raw rupee values, because the business question is about relative composition. Segments start at 12 o'clock for consistent visual reference.

**Mistake Avoided:** Did not use a 3D pie chart (which distorts slice angles and makes accurate comparison impossible). Did not create a pie chart for sub-categories (too many slices would make it unreadable — a bar chart would be more appropriate there).

---

## Chart 9: Heatmap — Returns by Customer Segment × Category

**Business Question:** Which combination of customer segment and product category drives the most returns?

**Why This Chart Type:**
A heatmap (matrix visualization) shows the intersection of two categorical variables using color intensity. It is the most compact way to show 3×3 = 9 combinations simultaneously. Darker color = higher returns immediately draws the eye to problem areas.

**Fields Used:**
- Rows: Customer Segment
- Columns: Category
- Color: Sequential red scale (lighter = fewer returns, darker = more returns)
- Label: Exact count in each cell

**Design Principle Applied:** Sequential color scale (single hue) is used because the data is unidirectional (0 to max returns). Adding cell labels ensures precision for viewers who need exact numbers.

**Mistake Avoided:** Did not use a grouped bar chart (would require 9 bars and make comparison across segments and categories much harder). Did not use diverging color (no "good vs bad" split — all returns are unwanted).

---

## Overall Dashboard Design Principles Applied

| Principle | Implementation |
|---|---|
| **Consistent color encoding** | Blue = Sales, Green = Profit, Orange = Furniture, Red = Loss/Alert throughout |
| **Minimal clutter** | Removed top and right spines from all charts; used light gridlines only on y-axis |
| **Clear hierarchy** | KPI cards at top for executive summary; detailed charts below |
| **Readable labels** | Font sizes 8–11pt; labels placed inside or near bars to reduce eye travel |
| **Sorted data** | Bars sorted by value for instant ranking; not alphabetically |
| **Reference lines** | Zero-profit line on scatter and sub-category charts to anchor loss/profit split |
| **Avoid 3D charts** | All charts are flat 2D; no 3D effects that distort proportions |
| **Consistent axis units** | Rs Millions used consistently across all monetary axes |
