# Supply-Chain-and-Logistic-Analysis
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Project Overview

This project presents an end-to-end analytical assessment of a supply chain and logistics operation, focusing on how purchasing behavior, inventory dynamics, and demand volatility interact to drive financial and operational outcomes.
Rather than reporting isolated KPIs, the analysis is structured to identify systemic inefficiencies, inventory risk concentrations, and decision points where data-driven intervention creates the highest impact.

By combining descriptive analytics, risk diagnostics, and forward-looking demand signals, the project demonstrates how supply chain performance can be improved through targeted actions, not blanket inventory expansion—balancing service level, working capital efficiency, and operational resilience.

![Project overview](./docs/porfolio_intro.png) 

# Project overview :

## Overview: the actual situation of the business.
![Overview](./screenshots/overview.png)

## Purchase & Supplier Analysis: What is the situation regarding suppliers, and which ones are performing effectively.
![Purchase & Supplier Analysis](./screenshots/purchase_supplier_analysis.png)

## Risk Analytics: risks in warehouses
![Risk Analytics](./screenshots/risk_analytic.png)

## Forecast the Trend: Forecasting commodity trends to make import decisions.
![Forecast the Trend](./screenshots/forecast_trend.png)

# Project objective

This project explores how operational supply chain data can be transformed into risk-focused insights rather than descriptive reporting.
The goal is to identify where inventory risk truly comes from, why it persists despite stable purchasing, and how decision-makers can respond in a targeted and cost-efficient way.

# Why this project matters

Many supply chain dashboards stop at showing what happened. This project goes further by answering:

Is inventory risk random or structural?

Is the problem driven by supply limitations or demand pressure?

Which segments should be prioritized to reduce stockout exposure fastest?

# What this project demonstrates

Translating transactional data into a problem-solving narrative

Combining BI dashboards with statistical validation

Framing insights in a way that supports real operational decisions, not just reporting

# Deliverables

Power BI dashboard for operational visibility

Excel-based analytical dataset to ensure correct granularity

Statistical testing in JASP to validate hypotheses

Consulting-style storyline suitable for decision-makers and interviews

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Below is the structured problem-solving analysis, presented across four logical steps:
Problem framing → Diagnostic approach → Key insights → So what & actions

# SLIDE 1 – OVERVIEW
Inventory pressure is driven by demand volatility, not insufficient purchasing

## What we see
Sales and purchases move at scale, but inventory levels fluctuate sharply over short periods. Large sales spikes are followed by rapid inventory drawdowns, while replenishment reacts with delay.

## What this means
The supply chain is not constrained by total purchasing capacity. Instead, it struggles to absorb demand volatility, causing temporary stock stress despite high overall procurement volumes.

## Why it matters
Treating this as a “buy more” problem would inflate working capital without fixing the root cause. The core issue is timing and alignment, not volume.

## So what
Inventory management must shift from volume-based planning to volatility-aware control, with closer monitoring of sales-driven shocks.

# SLIDE 2 – FORECAST & REORDER LOGIC
Forecast signals indicate near-term demand pressure that exceeds current reorder assumptions

## What we see
Short-term sales forecasts point to a sustained demand level that, when compared to current reorder thresholds, leaves limited buffer for unexpected spikes.

## What this means
Existing reorder points appear calibrated to historical averages rather than forward-looking demand signals. This creates exposure when demand accelerates faster than replenishment cycles.

## Why it matters
Without integrating forecast signals into reorder logic, the system systematically reacts after inventory risk has already materialized.

## So what
Reorder points should be dynamically adjusted using forecasted demand rather than static historical benchmarks, reducing reactive firefighting.

# SLIDE 3 – PURCHASE & SUPPLIER ANALYSIS
Supplier contribution is concentrated, amplifying dependency risk rather than stabilizing supply

## What we see
Purchasing volume is heavily concentrated among a limited number of vendors. While this supports scale efficiency, it also ties replenishment stability to a small supplier base.

## What this means
Inventory risk is partially structural: when high-volume vendors experience delays or mismatches in timing, downstream inventory volatility increases disproportionately.

## Why it matters
Supplier concentration magnifies operational risk, even if total purchase volumes remain strong.

## So what
The focus should move from total purchase optimization to supplier risk balancing, combining volume efficiency with resilience considerations.

# SLIDE 4 – INVENTORY RISK & LOW-STOCK EXPOSURE
Inventory risk is unevenly distributed, creating clear prioritization opportunities

## What we see
Low-inventory exposure and inventory variance are concentrated in a subset of items. Many products remain stable, while a smaller group drives the majority of risk.

## What this means
Inventory risk is not systemic across the portfolio. It is localized and predictable, enabling targeted intervention.

## Why it matters
Broad inventory increases would be inefficient. The highest return comes from addressing the small group of high-risk items driving volatility.

## So what
A risk-based inventory strategy—prioritizing high-variance, low-buffer items—can significantly reduce stockout exposure without increasing overall inventory levels.


# Strategic Summary – Supply Chain & Inventory
The situation

Despite strong purchasing volumes, the supply chain continues to face recurring inventory pressure and low-stock exposure. The issue is not insufficient supply capacity, but misalignment between demand volatility, replenishment timing, and inventory control logic.

# Key diagnosis

Demand volatility, rather than procurement volume, is the primary driver of inventory stress.

Reorder points are backward-looking, anchored in historical averages instead of forward demand signals.

Supplier contribution is highly concentrated, amplifying operational risk when timing mismatches occur.

Inventory risk is unevenly distributed, with a small subset of items driving the majority of low-inventory exposure.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Statistical Insights & Actionable Recommendations

![Descriptive](./screenshots/descriptive.png) 

## 1. Distribution & Outliers – Inventory and Sales

![Boxplot Overview](./screenshots/box_plot.png)

* Insight

Inventory and sales distributions are extremely right-skewed, indicating that a small fraction of SKUs drives a disproportionate share of volume.

* Evidence

- BeginOnHand
Median: 9 units
Mean: 30 units
Max: 467,200 units
Skewness: 173.2

- Sales
Median: $71.97
Mean: $218.8
Max: $20,410
Skewness: 12.29

* So what

Using averages to plan inventory will systematically overestimate required stock for most SKUs while failing to control risk for high-impact items.

* Action

- Classify SKUs into long-tail vs high-impact groups using percentiles

- Define inventory targets using P75 / P90 thresholds, not mean

- Apply tighter monitoring to the top 5–10% SKUs contributing the majority of stock and sales

## 2. Purchase–Sales Relationship

![Correlation](./screenshots/correlation.png)

![Correlation](./screenshots/t_test.png)

* Insight

Purchases and sales are strongly and linearly coupled, indicating reactive procurement behavior.

* Evidence

Pearson correlation: r = 0.88
Statistical significance: p < 0.001
95% CI: [0.877, 0.882]

* So what

Procurement volume closely follows realized sales, which amplifies demand shocks and increases inventory volatility during peak periods.

* Action

- Decouple purchasing decisions from realized sales

- Use forecasted demand as the primary trigger for replenishment

- Introduce demand smoothing (e.g. rolling averages or forecast bands)
- 
## 3. Inventory Structure – Clustering Analysis

![Clustering](./screenshots/clustering.png)

* Insight

Inventory behavior is highly heterogeneous and cannot be explained by a small number of clean segments.

* Evidence

Model-based clustering selected 10 clusters (BIC optimized)
Silhouette score: 0.15 (low separation)
Large variance in cluster sizes (from 242 to 8,031 records)

* What this actually means (plain language)

SKUs do not fall into neat, well-separated groups.
Instead, inventory behavior varies along multiple dimensions at once (volume, turnover, volatility).

* So what

- Applying a single replenishment rule across all SKUs will either:

- Overprotect low-risk items, or

- Under-protect volatile, high-risk items

* Action

- Replace pure clustering with a rule-based segmentation:

- Segment by Sales Volume × Inventory Volatility

** Example:

High sales / high volatility → frequent review, lower safety stock buffer

Low sales / low volatility → relaxed replenishment cycles

Use clustering as a diagnostic tool, not as the final decision rule

## 4. Sales Drivers – Regression Analysis

![Linear Regression](./screenshots/linear_regression.png)

* Insight

Sales performance is driven by flow efficiency, not by holding larger inventories.

* Evidence

Model explanatory power: R² = 0.786
Key coefficients (standardized):
Purchases → Sales: β = 0.856 (p < .001)
BeginOnHand → Sales: β = 0.131 (p < .001)
EndOnHand → Sales: β = -0.066 (p < .001)

* So what

Purchasing activity supports sales, but excess ending inventory reduces marginal sales impact, increasing holding costs without revenue upside.

* Action

- Define upper inventory bounds for slow-moving SKUs

- Shift KPIs from “stock level” to inventory turnover and flow rate

- Flag SKUs with rising EndOnHand but stagnant sales for markdown or delisting review
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Executive Recommendation Summary

## Key conclusion
Supply chain inefficiencies are structural, not volume-related.

## What to change

* From average-based planning → distribution-aware planning

* From reactive purchasing → forecast-led replenishment

* From uniform inventory rules → risk-segmented control

## Expected impact

* Reduced inventory volatility

* Lower capital tied in excess stock

* Improved service stability under demand shocks
