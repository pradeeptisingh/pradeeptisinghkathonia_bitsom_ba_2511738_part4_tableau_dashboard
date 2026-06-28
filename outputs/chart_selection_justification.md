# Chart Selection Justification

This document explains the chart type chosen for each major view in the executive dashboard, the design rationale, and visualization principles applied.

---

## 1. Sales Trend View — Line Chart (Dual-Axis)

**Question Answered:** How are total sales and profit trending month-over-month over 2024–2025?

**Why Line Chart:** A line chart is the canonical choice for time-series data. It naturally shows direction, magnitude, and rate of change across continuous time. Comparing two measures (Sales and Profit) using a dual-axis line chart allows leadership to see both scale and margin compression or expansion in a single view.

**Field Mappings:**
- X-axis: `Order Date` (Month/Year)
- Y-axis (left): `SUM(Sales)`
- Y-axis (right): `SUM(Profit)`
- Color: Blue for Sales, Green for Profit (distinct, colorblind-friendly)

**Design Principle Applied:** Pre-attentive attribute — color — differentiates the two measures without labels cluttering every data point. Gridlines are minimal (horizontal only) to reduce noise.

**Mistake Avoided:** Did not use a bar chart for this view (bars imply discrete comparisons, not continuous trends). Did not use stacked bars, which would obscure the profit line below sales.

---

## 2. Regional Performance View — Filled Map + Bar Chart

**Question Answered:** Which regions and states generate the most sales and profit?

**Why Filled Map:** Geographic data with state-level granularity is naturally suited to maps. A filled (choropleth) map lets leadership instantly see geographic concentration — darker color = higher value. This is more intuitive for spatial patterns than a table or bar chart alone.

**Why Supplemental Bar Chart:** A map alone cannot precisely rank regions or show exact values. A bar chart of the four regions (North, South, East, West) supplements the map with exact figures and easy ranking.

**Field Mappings (Map):**
- Geography: `State`
- Color: `SUM(Sales)` — sequential blue scale (light to dark)
- Tooltip: Sales, Profit, Profit Margin %

**Field Mappings (Bar Chart):**
- X-axis: `SUM(Sales)`
- Y-axis: `Region`
- Color: `Profit Margin` — diverging color (red = low margin, green = high)

**Design Principle Applied:** Spatial encoding for geography; color saturation for magnitude; sorting bars by descending sales for easy ranking.

**Mistake Avoided:** Did not use a pie chart for regional share — pies are poor for comparing more than 3 parts and make precise comparison difficult. Did not use 3D maps, which distort spatial perception.

---

## 3. Category Profitability View — Bar Chart (Horizontal, Sorted)

**Question Answered:** Which product categories and sub-categories drive or destroy profit?

**Why Horizontal Bar Chart:** With 13 sub-categories, a horizontal bar chart provides enough label space and easy comparison. Sorting by profit descending immediately reveals winners and losers.

**Why Show Negative Values:** Certain sub-categories (particularly some Furniture items at high discounts) generate negative profit on individual orders. The bar chart's ability to extend left of zero makes these losses instantly visible — crucial for executive decision-making.

**Field Mappings:**
- Y-axis: `Sub-Category`
- X-axis: `SUM(Profit)`
- Color: `Category` (three distinct colors: Furniture, Office Supplies, Technology)
- Label: `Profit Margin %` displayed on each bar

**Design Principle Applied:** Color by parent category creates natural grouping without needing a separate facet. Sorting enforces a performance ranking hierarchy.

**Mistake Avoided:** Did not use a treemap here (treemaps are better for showing proportional share, not margin comparisons). Did not use a pie chart (cannot show negative values or fine-grained ranking).

---

## 4. Customer Segment View — Grouped Bar Chart + KPI Cards

**Question Answered:** How do the three customer segments differ in sales volume, profit, and margin?

**Why Grouped Bar Chart:** Three segments, three measures (Sales, Profit, Margin) — a grouped bar chart places all metrics side by side for direct visual comparison. KPI cards above the chart highlight summary totals for quick scanning.

**Field Mappings:**
- X-axis: `Customer Segment`
- Y-axis: `SUM(Sales)` (primary bar), `SUM(Profit)` (secondary bar)
- Color: Segment color (consistent palette across dashboard)
- Labels: Margin % shown at top of each profit bar

**Design Principle Applied:** Consistent segment colors are reused across all views (e.g., Consumer = teal, Corporate = navy, Home Office = orange) to create visual coherence. KPI cards reduce cognitive load by surfacing totals.

**Mistake Avoided:** Did not use stacked bars (would obscure intra-segment comparisons). Did not use a scatter plot for three segments (too few data points for a scatter).

---

## 5. Shipping Performance View — Bar Chart + Box-and-Whisker Distribution

**Question Answered:** Which shipping modes cause the most delays, and how does delivery time distribute?

**Why Bar Chart for Average Delivery Days:** A simple horizontal bar chart ranked by average delivery days makes the comparison immediate — Standard Class's ~4.7-day average versus Same Day's ~0.4 days is stark and actionable.

**Why Distribution View:** Averages can hide outliers. A box plot or violin plot shows the full distribution — revealing that some Standard Class shipments take 6–7 days, not just the average.

**Field Mappings:**
- X-axis: `AVG(Delivery Days)`
- Y-axis: `Ship Mode`
- Color: Delivery performance bucket (green = fast, yellow = standard, red = slow)
- Detail: Delivery Days count per bucket

**Design Principle Applied:** Traffic-light color encoding (green/yellow/red) is universally understood in business contexts and requires no legend explanation.

**Mistake Avoided:** Did not use a line chart for this view (ship mode is categorical, not sequential). Did not sort alphabetically — sorted by delivery speed for business relevance.

---

## 6. Discount vs. Profit View — Scatter Plot

**Question Answered:** Is there a relationship between discount level and profit? Which products are most affected?

**Why Scatter Plot:** The relationship between two continuous variables (Discount % and Profit) is best visualized as a scatter plot. Each point represents an order, revealing the trend, clusters, and outliers simultaneously. A reference line at `Profit = 0` highlights which discount levels tip orders into losses.

**Field Mappings:**
- X-axis: `Discount`
- Y-axis: `Profit`
- Color: `Category` (distinguishes Furniture vs. Technology behavior)
- Size: `Sales` (larger bubbles = higher-value orders)
- Trend Line: Linear regression line to show direction of correlation

**Design Principle Applied:** Multi-attribute encoding (position, color, size) layers multiple dimensions without requiring separate charts. Trend line provides quantitative insight beyond visual impression.

**Mistake Avoided:** Did not aggregate discount into buckets and use a bar chart — this would lose the order-level variation that reveals the scatter pattern. Did not use a pie chart (wholly inappropriate for bivariate continuous data).

---

## 7. Return Analysis View — Heat Table (Highlight Table)

**Question Answered:** Which combinations of category, segment, or region have the highest return rates?

**Why Highlight Table:** A highlight table (also called a heat table or text table with color encoding) is ideal for cross-tabulated categorical data. With Category × Region as the two axes, the color intensity immediately surfaces the high-risk intersections without requiring the viewer to parse numbers.

**Field Mappings:**
- Rows: `Category`
- Columns: `Region`
- Color: `Return Rate` (light to dark red — higher = more returns)
- Label: `Return Rate %` displayed in each cell

**Design Principle Applied:** The highlight table preserves numeric precision (the text label) while also providing pre-attentive visual pop (the color). A manager can read the exact number or quickly scan the darkest cells.

**Mistake Avoided:** Did not use a bar chart for this (would require 12 separate bars, losing the cross-tab structure). Did not use pie charts per category/region (visually overwhelming and imprecise).

---

## Dashboard-Level Design Decisions

### Color Palette
- Technology: Navy Blue
- Furniture: Warm Orange
- Office Supplies: Slate Green
- Consistent segment and region colors applied across all sheets

### Layout Hierarchy
- KPI cards (Sales, Profit, Margin, Returns) at the top — most important, fastest to read
- Sales Trend below KPIs — sets context and narrative
- Regional Map and Category Bar in the second row — where? and what?
- Segment, Shipping, Discount, Returns in the third row — who? how? why?

### Filter Panel
- Region, Category, Customer Segment, Date Range, Ship Mode — all persistent across views
- At least one action filter (clicking a region on the map filters all other views)

### Minimal Clutter
- No 3D charts
- Gridlines only where necessary (horizontal, faint)
- Axis titles abbreviated; tooltips carry full detail
- No decorative images or icons that don't encode data
