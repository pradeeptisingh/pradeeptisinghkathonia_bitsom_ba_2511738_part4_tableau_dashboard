# Business Insights: Executive Sales Dashboard

## Calculated Fields Used in Tableau

| Calculated Field | Formula | Purpose |
|---|---|---|
| Profit Margin | `SUM([Profit]) / SUM([Sales])` | Measures profitability efficiency |
| Cost | `[Sales] - [Profit]` | Derives cost of goods sold |
| Average Order Value | `SUM([Sales]) / COUNTD([Order ID])` | Tracks spending per transaction |
| Return Rate | `SUM([Return Flag]) / COUNT([Order ID])` | Identifies product/segment risk |
| Shipping Delay Bucket | `IF [Delivery Days] = 0 THEN "Same Day" ELSEIF [Delivery Days] <= 2 THEN "Fast (1-2 days)" ELSEIF [Delivery Days] <= 4 THEN "Standard (3-4 days)" ELSE "Slow (5+ days)" END` | Groups delivery performance for analysis |

---

## Business Insights

### 1. Sales Trend – Consistent Growth with Seasonal Peaks

**Observation:** Monthly sales across 2024–2025 show peaks in Q3 (July–August) and Q4 (October–November), with softer periods in Q2 (April–June).

**Data Evidence:** July 2025: ₹10.66M, August 2025: ₹10.86M — among the highest months; April 2025 dips to ₹7.19M.

**Business Interpretation:** Seasonal demand spikes suggest that customers are buying more during mid-year and year-end periods, possibly aligned with corporate procurement cycles and festive/holiday preparation.

**Recommended Action:** Pre-position inventory and ramp marketing spend heading into July and October. Consider targeted promotions in April–June to smooth revenue dips.

---

### 2. Regional Performance – South Leads, West Lags Slightly

**Observation:** The South region generates the highest total sales (₹64.7M) and profit (₹9.99M), followed by North (₹54.6M), while East and West are closely matched around ₹48.9M each.

**Data Evidence:** South profit margin: 15.44%; West profit margin: 15.14% — differences are small but compounded over volume.

**Business Interpretation:** The South's stronger performance may reflect higher corporate density or better channel penetration. The West's slightly lower margin warrants a review of discount practices or product mix.

**Recommended Action:** Investigate the top-performing states in South (Telangana, Tamil Nadu, Karnataka) to replicate strategies in West (Maharashtra, Rajasthan, Goa).

---

### 3. Category Profitability – Technology Dominates; Furniture Is a Concern

**Observation:** Technology accounts for ₹153.9M in sales and ₹28.0M in profit (18.2% margin). Furniture delivers only a 6.9% margin despite ₹51.6M in sales.

**Data Evidence:** Furniture sub-categories Tables and Bookcases show margins below 6% — the weakest in the entire portfolio. Several Furniture orders show negative profit, particularly those with high discounts (30%+).

**Business Interpretation:** Furniture requires significant discounting to close sales, eroding margins. Technology products (Copiers, Accessories, Phones, Machines) all exceed 18% margin.

**Recommended Action:** Review Furniture pricing strategy. Set discount guardrails — no more than 20% on Tables and Bookcases. Consider bundling Furniture with high-margin Office Supplies.

---

### 4. Sub-Category Deep Dive – Copiers and Accessories Are Profit Engines

**Observation:** Copiers (₹40.6M sales, ₹7.3M profit) and Accessories (₹39.2M sales, ₹7.2M profit) are among the highest profit contributors. Paper and Binders, while low-volume, maintain ~15% margins.

**Data Evidence:** All Technology sub-categories (Machines, Phones, Accessories, Copiers) exceed 18% margin. All Furniture sub-categories remain below 9%.

**Business Interpretation:** Technology drives disproportionate profit. Office Supplies are reliable but low-scale. Furniture is a volume play with thin margins.

**Recommended Action:** Invest more in Technology category marketing and expand SKU range. Evaluate whether Furniture's revenue contribution justifies the margin drag.

---

### 5. Customer Segment Behavior – Home Office Leads Slightly

**Observation:** All three segments (Home Office, Corporate, Consumer) are closely matched in both sales (~₹70–74M) and margins (~15.2–15.5%).

**Data Evidence:** Home Office: ₹74.5M / 15.51% margin; Consumer: ₹71.9M / 15.34%; Corporate: ₹70.6M / 15.18%.

**Business Interpretation:** No single segment is dramatically outperforming. The near-equal distribution suggests balanced sales across all customer types, but small margin differences may compound at scale.

**Recommended Action:** Develop segment-specific retention campaigns. Home Office customers may respond to bundle deals; Corporate may need volume discounts. Consider loyalty programs to deepen each segment.

---

### 6. Discount Impact – Heavy Discounting Destroys Profit

**Observation:** Orders with no discount average ₹13,203 in profit per order. Orders in the High (21%+) discount tier average only ₹2,915 — a 78% reduction in profit per order.

**Data Evidence:** No Discount orders total ₹13.5M in profit on ₹65.8M in sales (20.5%). High Discount orders total ₹3.4M on ₹45.0M in sales (7.5%).

**Business Interpretation:** Aggressive discounting — especially 30%+ levels seen on Furniture and some Office Supplies — dramatically reduces returns. The volume gain does not compensate for the margin erosion.

**Recommended Action:** Implement a discount approval workflow for orders above 20%. Train sales staff to use non-discount levers such as bundle deals, extended payment terms, or added services.

---

### 7. Shipping & Delivery Performance – Standard Class Creates Longest Delays

**Observation:** Standard Class shipping averages 4.71 delivery days — nearly 3x more than Same Day (0.40 days) and 2.7x more than First Class (1.77 days). Yet Standard Class is the most used mode.

**Data Evidence:** Average profit per order by mode: Same Day ₹9,102; First Class ₹7,364; Second Class ₹8,261; Standard Class ₹7,839. Same Day and Second Class produce higher per-order profit despite service differences.

**Business Interpretation:** Over-reliance on Standard Class may be hurting customer experience. Same Day generates higher average order values and profit — suggesting premium customers prefer faster shipping.

**Recommended Action:** For high-value orders above ₹50,000, default to First Class or Same Day and position it as a value-add. Review Standard Class agreements with logistics partners to reduce the 4–7 day tail.

---

### 8. Return Patterns – Furniture Has Alarming Return Rate

**Observation:** Furniture has a 7.67% return rate — more than double Office Supplies (3.65%) and Technology (3.03%).

**Data Evidence:** Of 1,147 Furniture orders, 88 were returned. Sub-categories with higher discounts also appear more frequently in returns.

**Business Interpretation:** Furniture returns may be driven by product quality concerns, misleading descriptions, or customer remorse after heavy discounting. High-discount orders may attract buyers who later regret the purchase.

**Recommended Action:** Conduct a root cause analysis on Furniture returns. Improve product descriptions and images. Consider a restocking fee policy for non-defective returns above a value threshold to discourage frivolous returns.

---

### 9. Business Risk – Compounding Discount + Return Effect in Furniture

**Observation:** Furniture simultaneously has the lowest margins AND the highest return rate. This creates a double-loss scenario — revenue is discounted upfront and then reversed on return.

**Data Evidence:** Furniture margin: 6.89% overall; return rate: 7.67% — both the worst in the portfolio.

**Business Interpretation:** A Furniture order that is returned represents negative ROI once picking, packing, shipping, and return logistics are factored in.

**Recommended Action:** Urgent review of Furniture sales strategy needed. Short-term: cap discounts, add a return policy. Long-term: review supplier quality and whether the category should be maintained or repositioned.

---

### 10. Campaign Channel Opportunity – Referral Underutilized

**Observation:** Referral as a campaign channel has very limited order volume compared to Organic and Social, yet referral-driven customers tend to have higher order values (based on data patterns).

**Business Interpretation:** Referral programs are typically low-cost and high-trust. The current underinvestment may represent a missed acquisition channel.

**Recommended Action:** Launch a structured referral incentive program. Offer existing customers a discount voucher for each successful referral. Target Home Office and Corporate segments who tend to influence their networks.
