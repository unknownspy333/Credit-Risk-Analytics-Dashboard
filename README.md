# Credit Risk Analytics Dashboard

An end-to-end banking credit risk analysis built in **Power BI**, with **Python** visuals for the statistical layer. The report profiles a 12,000-loan portfolio across five regions and five loan products, and surfaces the drivers behind default behaviour.

**Author:** Pratik Thombre

---

## Overview

The dashboard answers four questions a credit risk team would actually ask:

1. How healthy is the portfolio right now?
2. Which regions and loan products carry the most exposure?
3. What financial variables actually drive risk?
4. How do approved and defaulted borrowers differ statistically?

Each question maps to one report page.

---

## Dashboard Pages

### 1. Executive Credit Risk Overview
Portfolio health at a glance — total loans issued, total portfolio value, default rate, and average credit score, alongside loan volume by year, credit score distribution, and loan status split.

![Executive Credit Risk Overview](screenshots/page1_executive.png)

### 2. Regional Risk & Portfolio Dynamics
Regional loan growth over time (animated bar chart race), default rate comparison by region, a region × loan purpose risk intensity matrix, and an income vs loan exposure scatter.

![Regional Risk and Portfolio Dynamics](screenshots/page2_regional.png)

### 3. Advanced Credit Risk Intelligence
Risk driver analysis — correlation matrix of financial variables, debt-to-income impact on loan size, risk category distribution over time, and a region slicer to cut every visual by geography.

![Advanced Credit Risk Intelligence](screenshots/page3_risk.png)

### 4. Advanced Statistical & Relationship Analysis (Python)
Four Python visuals embedded directly in Power BI: a multi-variable pair plot, a credit score violin distribution by loan status, a correlation heatmap, and a region–loan purpose network graph.

![Advanced Statistical and Relationship Analysis](screenshots/page4_python.png)

---

## Dataset

`data/Banking_Credit_Risk_Dataset.csv` — 12,000 loan records, 22 columns, no missing values.

| Group | Fields |
|---|---|
| Customer | `Customer_ID`, `Age`, `Gender`, `Marital_Status`, `Education_Level`, `Employment_Type`, `Dependents`, `Region` |
| Financial | `Annual_Income`, `Credit_Score`, `Account_Balance`, `Existing_Loans_Count`, `Debt_to_Income_Ratio_%` |
| Loan | `Loan_ID`, `Loan_Purpose`, `Loan_Amount`, `Loan_Term_Months`, `Interest_Rate`, `Application_Date`, `Approval_Date` |
| Target | `Loan_Status`, `Default_Risk_Flag` |

- **Period:** January 2018 – June 2023
- **Regions:** Central, East, North, South, West
- **Loan purposes:** Home, Personal, Education, Business, Car
- **Portfolio value:** ~₹9.38bn
- **Average credit score:** 595.75

> **Note on the data:** this is a simulated dataset, and the class balance is heavily skewed — 11,954 records are flagged as defaults against 46 approvals. It works well for exposure profiling and relationship analysis, but it is not a realistic base for training a predictive default model without resampling.

---

## Repository Structure

```
Credit-Risk-Analytics-Dashboard/
├── data/
│   └── Banking_Credit_Risk_Dataset.csv
├── powerbi/
│   └── Credit_Risk_Dashboard.pbix
├── python/
│   ├── advanced_correlation_heatmap.py
│   ├── credit_score_violin_distribution.py
│   ├── financial_correlation_heatmap.py
│   ├── loan_purpose_relationship_network.py
│   └── pairplot_risk_analysis.py
├── screenshots/
│   ├── page1_executive.png
│   ├── page2_regional.png
│   ├── page3_risk.png
│   └── page4_python.png
└── README.md
```

---

## Tools & Techniques

- **Power BI Desktop** — data model, DAX measures, report design
- **DAX** — default rate, high-risk customer percentage, average debt-to-income ratio, risk category banding
- **Python (in Power BI)** — pandas, seaborn, matplotlib, networkx
- **Power Query** — data shaping and type handling
- **Custom visual** — bar chart race for animated time-series comparison

---

## Running It Locally

**Prerequisites**

- Power BI Desktop (recent version)
- Python 3.8+ available to Power BI

```bash
pip install pandas seaborn matplotlib networkx
```

**Steps**

1. Clone the repository.
2. Open `powerbi/Credit_Risk_Dashboard.pbix` in Power BI Desktop.
3. Point the Python scripting home at your Python install under **File → Options and settings → Options → Python scripting**.
4. If the data source path breaks, update it under **Transform data → Data source settings** to your local copy of `data/Banking_Credit_Risk_Dataset.csv`.
5. Refresh.

**About the Python scripts**

The files in `python/` are written for the Power BI Python visual, which injects a DataFrame named `dataset` containing the fields dragged into the visual. They have no `read_csv` call by design. To run one standalone, add this at the top:

```python
import pandas as pd
dataset = pd.read_csv("data/Banking_Credit_Risk_Dataset.csv")
```

The heatmap and pair plot scripts expect numeric columns only, so subset the frame before calling them outside Power BI.

---

## Key Observations

- Credit score alone separates the two loan statuses poorly — the violin plot shows overlapping distributions, so no single-threshold cutoff would work as a decision rule.
- Debt-to-income ratio and loan amount move together (~0.49 correlation), while annual income and debt-to-income ratio move against each other (~-0.61) — the strongest relationships in the matrix.
- Default rates sit close to portfolio-wide levels in every region, so geography is a weak standalone signal here; the region × loan purpose matrix is more informative than either dimension on its own.
- Loan volume holds steady from 2018 through 2022 and drops sharply in 2023, which reflects the dataset ending mid-year rather than a real contraction.

---

## Possible Extensions

- Resample the target and fit a logistic regression or gradient boosting model for default prediction
- Add a what-if parameter for interest rate sensitivity
- Build a vintage analysis view by origination cohort
- Publish to Power BI Service with scheduled refresh

---

## Contact

**Pratik Thombre**

Feedback and suggestions are welcome — open an issue or reach out.
