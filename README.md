# Olist E-Commerce SQL Analysis

An end-to-end SQL analysis of **100,000+ orders** from the Olist Brazilian E-Commerce dataset, answering five core business questions about revenue, growth, retention, and customer value.

---

##  Business Questions Answered

1. **Which product categories drive the most revenue?**
2. **How has monthly revenue trended over time?**
3. **How are customers segmented by RFM (Recency, Frequency, Monetary)?**
4. **What is month-over-month cohort retention?**
5. **How is customer lifetime value distributed?**

---

## creat Stack

- **PostgreSQL 18** — relational database
- **pgAdmin 4** — SQL client
- **SQL** — CTEs, window functions, multi-table joins, cohort logic

---

##  Project Structure


olist_ecommerce/
├── schema/
│ └── create_tables.sql
├── queries/
│ ├── 01_top_categories.sql
│ ├── 02_monthly_revenue.sql
│ ├── 03_rfm_segmentation.sql
│ ├── 04_cohort_retention.sql
│ └── 05_customer_lifetime_value.sql
├── insights/
│ └── findings.md
├── .gitignore
└── README.md


---

## 📊 Key Findings

### 1. Revenue Concentration (Pareto Pattern)

The top 7 product categories drive **~50% of total revenue**.

| Rank | Category | Revenue (R$) | % of Total |
|---|---|---|---|
| 1 | health_beauty | 1,233,131 | 9.33% |
| 2 | watches_gifts | 1,166,176 | 8.82% |
| 3 | bed_bath_table | 1,023,434 | 7.74% |
| 4 | sports_leisure | 954,852 | 7.22% |
| 5 | computers_accessories | 888,724 | 6.72% |
| 6 | furniture_decor | 711,927 | 5.38% |
| 7 | housewares | 615,628 | 4.66% |

**Insight:** `watches_gifts` earns high revenue at low volume (high-ticket). `bed_bath_table` earns high revenue at high volume (workhorse). `health_beauty` leads on both.

---

### 2. Growth Plateau

Revenue scaled from **~R$10K/month (Sep 2016)** to **~R$900K/month (2018)** — a 20x increase in under 2 years.

**But growth stalled from April 2018 onwards.** Month-over-month growth dropped to near 0%:

| Month | Revenue (R$) | MoM Growth |
|---|---|---|
| 2017-11 (Black Friday) | 987,765 | +52.37% |
| 2017-12 | 726,033 | -26.50% |
| 2018-01 | 924,645 | +27.36% |
| 2018-04 | 973,534 | +2.12% |
| 2018-05 | 977,544 | +0.41% |
| 2018-06 | 856,077 | -12.43% |
| 2018-07 | 867,953 | +1.39% |
| 2018-08 | 838,576 | -3.38% |

**Insight:** The business hit a plateau. It stopped growing.

---

### 3. Retention Crisis (Headline Finding)

**Month-1 cohort retention is under 1% across almost all cohorts.** Over 99% of customers never return.

| Cohort | Cohort Size | Month-1 Returners | Retention % |
|---|---|---|---|
| 2017-01 | 717 | 2 | 0.28% |
| 2017-05 | 3,451 | 16 | 0.46% |
| 2017-08 | 4,057 | 28 | 0.69% |
| 2017-10 | 4,328 | 31 | 0.72% (highest) |
| 2017-11 | 7,060 | 40 | 0.57% |
| 2018-01 | 6,842 | 23 | 0.34% |
| 2018-04 | 6,582 | 39 | 0.59% |
| 2018-06 | 5,878 | 25 | 0.43% |

**Corroborated by RFM analysis:** Average order frequency is **~1.05 across ALL segments**. The "Loyal" segment represents only 5% of revenue.

**Insight:** Olist acquires customers who buy once and never return. This is a **structural retention problem**, not a data issue.

---

### 4. Customer Value is Pareto-Distributed

| Tier | Customers | Revenue (R$) | % of Revenue | Avg Value (R$) |
|---|---|---|---|---|
| Low Value (R$100–499) | 36,258 | 6,990,620 | 52.87% | 192.80 |
| Minimal (<R$100) | 53,466 | 2,855,757 | 21.60% | 53.41 |
| Mid Value (R$500–999) | 2,693 | 1,852,176 | 14.01% | 687.77 |
| High Value (R$1000+) | 941 | 1,522,945 | 11.52% | 1,618.43 |

**Insight:**
- **941 customers (0.9% of base)** drive **11.52% of revenue**
- **3,634 customers (3.7% of base)** drive **25.5% of revenue**
- **53,466 customers (55% of base)** drive only **21.6%** — the long tail

---

### 5. Comparison with Python Project

| Metric | Olist (SQL) | Online Retail II (Python) |
|---|---|---|
| Month-1 retention | **<1%** | ~21.2% |
| Business model | Marketplace | Wholesale / giftware |
| Repeat behavior | Rare | Common |
| Dataset size | 100k+ orders | 1M+ transactions |

**Insight:** The retention difference is a **business-model issue**, not a data quality issue.

---

##  Recommendations

1. **Stop over-investing in acquisition.** The business scaled 20x but retention stayed near zero. Filling a leaking bucket faster doesn't fix the leak.
2. **Investigate seller-level retention.** In a marketplace, customers may be loyal to *sellers*, not the *platform*.
3. **Launch a premium loyalty program** for the top 3.7% of customers who drive 25% of revenue.
4. **Low-cost reactivation campaign** for the long tail (55% of customers generating 21% of revenue).
5. **Re-examine the 2018 plateau.** With retention <1%, the company cannot grow via acquisition alone.

---

## 🚀 How to Reproduce

1. Install **PostgreSQL 18** and **pgAdmin 4**
2. Create a database named `olist_ecommerce`
3. Run `schema/create_tables.sql` in pgAdmin Query Tool
4. Download the [Olist Brazilian E-Commerce dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) from Kaggle
5. Import the 8 CSV files into their matching tables (skip `olist_geolocation_dataset.csv`)
6. Run each query in the `queries/` folder using pgAdmin Query Tool

---

##  SQL Skills Demonstrated

- **Multi-table joins** (up to 4 tables in one query)
- **CTEs** (`WITH ... AS`) for modular, readable queries
- **Window functions:** `LAG()`, `NTILE()`, `SUM() OVER ()`
- **Cohort analysis** with date arithmetic
- **RFM segmentation** in pure SQL
- **Pareto / CLV distribution** analysis
- **`NULLIF` and `COALESCE`** for safe division and null handling
- **Date functions:** `DATE_TRUNC`, `EXTRACT`, `TO_CHAR`

---

##  Contact

- **Portfolio:** [sandilenkosi12.github.io/DATA-ANALYST-PORTFOLIO](https://sandilenkosi12.github.io/DATA-ANALYST-PORTFOLIO/)
- **GitHub:** [github.com/sandilenkosi12](https://github.com/sandilenkosi12)
- **Email:** abelnkosi2000@gmail.com
