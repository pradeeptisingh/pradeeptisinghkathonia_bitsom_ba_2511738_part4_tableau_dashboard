# Tableau Workbook Build Instructions

The file `executive_dashboard.twbx` must be created manually in Tableau Desktop.

## Setup Steps

1. Open Tableau Desktop
2. Connect to Data → Microsoft Excel → select `data/dashboard_sales_data.xlsx`
3. Drag `dashboard_sales_data` sheet to the canvas
4. Set field types:
   - `order_date`, `ship_date` → Date
   - `state`, `city`, `region` → Geographic Role (State/Province, City)
   - `return_flag` → Number (whole)
   - `sales`, `profit`, `discount`, `delivery_days`, `quantity` → Measure (Number)

## Calculated Fields to Create (Ctrl+Shift+A or Analysis menu)

```
Profit Margin:       SUM([Profit]) / SUM([Sales])
Cost:                [Sales] - [Profit]
Average Order Value: SUM([Sales]) / COUNTD([Order ID])
Return Rate:         SUM([Return Flag]) / COUNT([Order ID])
Shipping Delay Bucket:
    IF [Delivery Days] = 0 THEN "Same Day"
    ELSEIF [Delivery Days] <= 2 THEN "Fast (1-2 days)"
    ELSEIF [Delivery Days] <= 4 THEN "Standard (3-4 days)"
    ELSE "Slow (5+ days)"
    END
Discount Tier:
    IF [Discount] = 0 THEN "No Discount"
    ELSEIF [Discount] <= 0.10 THEN "Low (≤10%)"
    ELSEIF [Discount] <= 0.20 THEN "Medium (11-20%)"
    ELSE "High (>20%)"
    END
```

## Required Sheets

1. **Sales Trend** — Line chart: Order Date (Month) on Columns, SUM(Sales) + SUM(Profit) dual-axis on Rows
2. **Regional Performance** — Filled map of State with SUM(Sales) color; Bar chart of Region vs SUM(Sales)
3. **Category Profitability** — Horizontal bar chart: Sub-Category on Rows, SUM(Profit) on Columns, Color = Category
4. **Customer Segment View** — Bar chart: Customer Segment on Columns, SUM(Sales)/SUM(Profit) on Rows
5. **Shipping Performance** — Bar chart: Ship Mode on Rows, AVG(Delivery Days) on Columns, Color = Shipping Delay Bucket
6. **Discount vs Profit** — Scatter plot: Discount on Columns, Profit on Rows, Color = Category, Size = Sales
7. **Return Analysis** — Highlight table: Category on Rows, Region on Columns, Color = Return Rate

## Executive Dashboard

1. Create a new Dashboard sheet
2. Set size to 1400×900 (desktop landscape)
3. Add KPI text objects at top: Total Sales, Total Profit, Profit Margin, Return Rate, Average Order Value
4. Arrange sheets per layout described in README
5. Add filters: Region, Category, Customer Segment, Order Date, Ship Mode
6. Add map-click action filter: Source = Regional Performance, Target = all sheets

## Save As

File → Export Packaged Workbook → save as `executive_dashboard.twbx`
