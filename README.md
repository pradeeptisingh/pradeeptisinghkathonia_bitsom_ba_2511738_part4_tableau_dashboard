# Part 4: Tableau Executive Dashboard
## Retail Sales Performance Analysis (2024–2025)

---

## Business Problem Summary

The retail leadership team needs a centralized executive dashboard to monitor business health across sales performance, profitability, customer segments, product categories, shipping efficiency, discounting behavior, and return patterns. The dashboard must go beyond raw metrics to tell a clear business story and identify actionable opportunities and risks.

---

## Dataset Description

**File:** `data/dashboard_sales_data.xlsx`  
**Rows:** 4,200 orders  
**Date Range:** January 1, 2024 – December 31, 2025

| Field | Type | Description |
|---|---|---|
| order_id | String | Unique order identifier |
| order_date | Date | Date order was placed |
| ship_date | Date | Date order was shipped |
| customer_id | String | Unique customer identifier |
| customer_segment | Categorical | Consumer, Corporate, Home Office |
| region | Categorical | North, South, East, West |
| state | Categorical | 19 Indian states |
| city | Categorical | City of delivery |
| category | Categorical | Furniture, Office Supplies, Technology |
| sub_category | Categorical | 13 sub-categories (Chairs, Copiers, Phones, etc.) |
| product_name | String | Individual product name |
| ship_mode | Categorical | Same Day, First Class, Second Class, Standard Class |
| sales | Numeric | Revenue per order (₹) |
| quantity | Integer | Units ordered |
| discount | Numeric | Discount rate (0–0.35) |
| profit | Numeric | Profit per order (₹, can be negative) |
| return_flag | Binary | 1 = returned, 0 = not returned |
| delivery_days | Integer | Days between order and delivery |
| customer_rating | Numeric | Rating given by customer (1–5) |
| campaign_channel | Categorical | Organic, Social, Email, Paid, Referral |

**Assumptions:**
- Dates stored as Excel serial numbers were converted to proper date format in Tableau
- `return_flag = 1` indicates a confirmed return; flag = 0 includes both kept orders and orders with no return data
- `campaign_channel` contains some nulls (~2–3% of records); these are excluded from channel-specific analysis
- All currency values are in Indian Rupees (₹)
- Negative profit values represent genuine loss-making orders (e.g., high-discount Furniture)

---

## Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`

The packaged workbook contains one executive dashboard and the following supporting sheets:

| Sheet Name | Purpose |
|---|---|
| Sales Trend | Line chart of monthly sales and profit over 2024–2025 |
| Regional Performance | Filled map of sales by state + bar chart by region |
| Category Profitability | Horizontal bar chart of profit by sub-category, colored by category |
| Customer Segment View | Grouped bars comparing segments on sales, profit, margin |
| Shipping Performance | Bar chart of average delivery days by ship mode |
| Discount vs Profit | Scatter plot showing discount rate vs. profit per order |
| Return Analysis | Highlight table of return rate by category × region |
| Executive Dashboard | Master dashboard combining all views with KPIs and filters |

---

## Calculated Fields Created

| Field Name | Formula | Purpose |
|---|---|---|
| **Profit Margin** | `SUM([Profit]) / SUM([Sales])` | Profitability ratio per view aggregation |
| **Cost** | `[Sales] - [Profit]` | Derives cost of goods sold (COGS) per order |
| **Average Order Value** | `SUM([Sales]) / COUNTD([Order ID])` | Tracks revenue intensity per unique order |
| **Return Rate** | `SUM([Return Flag]) / COUNT([Order ID])` | Percentage of orders returned |
| **Shipping Delay Bucket** | `IF [Delivery Days] = 0 THEN "Same Day" ELSEIF [Delivery Days] <= 2 THEN "Fast (1-2 days)" ELSEIF [Delivery Days] <= 4 THEN "Standard (3-4 days)" ELSE "Slow (5+ days)" END` | Groups delivery performance into human-readable tiers |
| **Discount Tier** | `IF [Discount] = 0 THEN "No Discount" ELSEIF [Discount] <= 0.1 THEN "Low (≤10%)" ELSEIF [Discount] <= 0.2 THEN "Medium (11-20%)" ELSE "High (>20%)" END` | Buckets discount levels for impact analysis |

---

## Dashboard Components

### KPI Cards (Top Row)
- Total Sales (₹217M)
- Total Profit (₹33.3M)
- Overall Profit Margin (15.3%)
- Return Rate (4.5%)
- Average Order Value

### Charts / Views
1. Sales Trend (line chart — dual axis, monthly)
2. Regional Performance (filled map + bar chart)
3. Category & Sub-Category Profitability (horizontal bar chart)
4. Customer Segment Comparison (grouped bar chart)
5. Shipping Mode Performance (bar chart with delay buckets)
6. Discount vs. Profit Impact (scatter plot)
7. Return Rate by Category × Region (highlight/heat table)

---

## Filters and Interactions

### Dashboard-Level Filters
- **Region** — filters all views to selected region(s)
- **Category** — narrows down to Furniture, Office Supplies, or Technology
- **Customer Segment** — filter by Consumer, Corporate, or Home Office
- **Order Date Range** — date slider to select time window
- **Ship Mode** — filter views by shipping mode

### Action Filters (Interactivity)
- **Map Click → Filter All Views:** Clicking a state on the regional map filters all other dashboard views to that state
- **Category Bar → Filter Sub-category:** Clicking a category in the profitability view highlights sub-categories within that category

---

## Key Business Insights

1. **Technology** drives 84% of total profit at 18%+ margin — the core business engine
2. **Furniture** generates only 6.89% margin with 7.67% return rate — double risk of loss
3. **South region** leads in sales (₹64.7M) and profit (₹9.99M)
4. **Discounts above 20%** reduce profit per order by 78% — urgent guardrail needed
5. **Standard Class shipping** averages 4.71 days — far behind alternatives
6. **Home Office** segment has the highest margin (15.51%) — underserved growth opportunity
7. **Sub-categories Tables and Bookcases** have sub-6% margins — pricing review required
8. **Referral channel** is underutilized relative to its potential
9. **Sales peaks** in July–August and October–November — seasonal plan needed
10. **Returned Furniture orders** represent near-certain net losses after operational costs

---

## Dashboard Story Summary

The business is healthy at the top line (₹217M revenue, 15.3% margin) but masks significant structural imbalances. Technology's excellent economics are subsidizing Furniture's poor performance. Aggressive discounting, concentrated in Furniture and Standard Class logistics delays, are the two most controllable levers to improve profitability in the near term. The South region and Home Office segment represent the strongest foundations to build from. See `outputs/dashboard_story.md` for the full narrative.

---

## Assumptions and Limitations

- No customer retention/cohort data available — cannot assess churn
- Campaign channel has ~2–3% null values excluded from channel analysis
- Return reasons not captured — root cause analysis requires additional data
- All monetary values in Indian Rupees (₹); no currency conversion applied
- Delivery days represents total calendar days, not business days
- Negative profit orders are included in all aggregations (not filtered out)


---

## Screenshots Included

| File | Description |
|---|---|
| `screenshots/full_dashboard.png` | Complete executive dashboard with all views |
| `screenshots/sales_trend_view.png` | Monthly sales and profit trend line chart |
| `screenshots/regional_performance_view.png` | State-level map and regional bar chart |
| `screenshots/category_profitability_view.png` | Sub-category profitability bar chart |
| `screenshots/filter_interaction_view.png` | Dashboard with region filter applied (South selected) |
