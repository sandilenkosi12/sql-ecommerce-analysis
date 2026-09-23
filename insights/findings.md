# Key Findings — Olist E-Commerce SQL Analysis

## 1. Revenue Concentration (Pareto)
Top 7 product categories drive ~50% of total revenue.
- health_beauty: R$1.23M (9.33%)
- watches_gifts: R$1.17M (8.82%)
- bed_bath_table: R$1.02M (7.74%)

## 2. Growth Then Plateau
Revenue scaled from ~R$10K/month (2016) to ~R$900K/month (2018).
Growth stalled from April 2018 onward (MoM growth ~0%).
Black Friday 2017 was the single peak month (R$987K, +52% MoM).

## 3. Structural Retention Crisis (Headline Finding)
Month-1 cohort retention is **under 1% across almost all cohorts**.
Olist acquires customers who buy once and never return.

Evidence:
- 2017-01 cohort (717 customers): 0.28% returned in month 1
- 2017-11 cohort (7,060 customers): 0.57% returned in month 1
- 2018-01 cohort (6,842 customers): 0.34% returned in month 1

This is corroborated by RFM analysis:
- Average order frequency is ~1.05 across ALL segments
- "Loyal" segment represents only 5% of revenue

## 4. Comparison with Online Retail II (Python Project)
| Metric | Olist (SQL) | Online Retail II (Python) |
|---|---|---|
| Month-1 retention | <1% | ~21.2% |
| Business model | Marketplace | Wholesale/giftware |
| Repeat behavior | Rare | Common |

Conclusion: Olist's retention problem is a business-model
issue, not a data quality issue.

## 5. Recommendation
Stop over-investing in acquisition. Investigate:
- Post-purchase engagement (email, loyalty program)
- Seller-level retention (are customers returning to the same seller?)
- Product category retention (do some categories have repeat buyers?)