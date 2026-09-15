# Credit Risk Analytics Dashboard

An end-to-end credit risk analytics project built in **Power BI** with **Python** visuals, covering 12,000 loan applications across five regions. The dashboard tracks portfolio health, regional risk concentration, and the financial drivers behind borrower default.

**Author:** Devaraju K G

---

## Overview

Lenders need to know three things quickly: how much money is at risk, where it is concentrated, and which borrower attributes predict default. This project answers all three across four report pages, moving from a high-level executive summary down to statistical relationship analysis.

The dataset is synthetic and generated for demonstration purposes, so the figures are not drawn from a real lending book. It is built to exercise the full analytics workflow — data modelling, DAX measures, interactive filtering, and Python-based exploratory analysis — rather than to describe an actual portfolio.

---

## Dashboard Pages

### 1. Executive Credit Risk Overview

Portfolio-level KPIs and distribution summaries: total loans issued, total portfolio value, default rate, and average credit score, alongside loan volume by year, credit score distribution, and loan status split.

![Executive Credit Risk Overview](screenshots/page1_executive.png)

### 2. Regional Risk & Portfolio Dynamics

Regional comparison of loan growth and default behaviour, including an animated portfolio growth race by region and year, a default risk intensity matrix cut by region and loan purpose, and an income-versus-loan-exposure scatter.

![Regional Risk & Portfolio Dynamics](screenshots/page2_regional.png)

### 3. Advanced Credit Risk Intelligence

Risk driver analysis with a region slicer, high-risk customer percentage, average debt-to-income ratio, a financial variable correlation matrix, and risk category distribution over time.

![Advanced Credit Risk Intelligence](screenshots/page3_risk.png)

### 4. Advanced Statistical & Relationship Analysis (Python)

Four Python visuals embedded directly in the report: a multi-variable pair plot, a credit score violin distribution by loan status, a correlation heatmap, and a region-to-loan-purpose network graph.

![Advanced Statistical & Relationship Analysis](screenshots/page4_python.png)

---

## Repository Structure

```
Credit-Risk-Analytics-Dashboard/
├── data/
│   └── Banking_Credit_Risk_Dataset.csv      # 12,000 loan records, 22 fields
├── powerbi/
│   └── Credit_Risk_Dashboard.pbix           # Power BI report file
├── python/
│   ├── advanced_correlation_heatmap.py      # Annotated correlation matrix
│   ├── financial_correlation_heatmap.py     # Base correlation matrix
│   ├── credit_score_violin_distribution.py  # Credit score by loan status
│   ├── pairplot_risk_analysis.py            # Multi-variable pair plot
│   └── loan_purpose_relationship_network.py # Region / loan purpose network
├── screenshots/
│   ├── page1_executive.png
│   ├── page2_regional.png
│   ├── page3_risk.png
│   └── page4_python.png
└── README.md
```

---

## Dataset

`data/Banking_Credit_Risk_Dataset.csv` — 12,000 rows, 22 columns, application dates spanning January 2018 to June 2023.

| Column | Description |
| --- | --- |
| `Customer_ID` | Unique customer identifier |
| `Age` | Borrower age (21–65) |
| `Gender` | Male / Female |
| `Marital_Status` | Single, Married, Divorced, Widowed |
| `Education_Level` | High School, Bachelor, Master, PhD |
| `Employment_Type` | Salaried, Self-Employed, Business, Unemployed |
| `Annual_Income` | Reported yearly income |
| `Region` | North, South, East, West, Central |
| `Credit_Score` | Credit score (300–900) |
| `Existing_Loans_Count` | Number of loans already held |
| `Dependents` | Number of dependents |
| `Account_Balance` | Current account balance |
| `Loan_ID` | Unique loan identifier |
| `Loan_Purpose` | Home, Personal, Car, Business, Education |
| `Loan_Amount` | Principal amount |
| `Loan_Term_Months` | Term length (12–120 months) |
| `Interest_Rate` | Annual rate (5%–18%) |
| `Debt_to_Income_Ratio_%` | Debt as a percentage of income |
| `Application_Date` | Date the loan was applied for |
| `Approval_Date` | Date the decision was recorded |
| `Loan_Status` | Approved / Default |
| `Default_Risk_Flag` | Binary default indicator (0 / 1) |

---

## Tools Used

- **Power BI Desktop** — data model, DAX measures, report pages, slicers and drill-through
- **Python 3** — statistical visuals rendered inside Power BI
- **pandas**, **seaborn**, **matplotlib**, **networkx** — analysis and plotting

---

## Getting Started

### View the dashboard

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
2. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/Credit-Risk-Analytics-Dashboard.git
   ```
3. Open `powerbi/Credit_Risk_Dashboard.pbix`.
4. If the data source path does not resolve, go to **Transform Data → Data source settings** and point it at your local copy of `data/Banking_Credit_Risk_Dataset.csv`.

### Run the Python visuals

The scripts in `python/` are written for the **Power BI Python visual**, which supplies a DataFrame named `dataset` at runtime. To run them in Power BI, enable Python scripting under **File → Options → Python scripting** and set your interpreter path.

Install the dependencies first:

```bash
pip install pandas seaborn matplotlib networkx
```

To run a script outside Power BI, load the CSV into a `dataset` variable before the plotting code:

```python
import pandas as pd
dataset = pd.read_csv("data/Banking_Credit_Risk_Dataset.csv")
```

Note that the correlation and pair plot scripts expect numeric columns only, so select the relevant fields (for example `Annual_Income`, `Loan_Amount`, `Credit_Score`, `Interest_Rate`, `Debt_to_Income_Ratio_%`) as Power BI does when building the visual.

---

## Key Analytical Themes

- **Portfolio exposure** — total lending value, loan volume trend, and concentration by credit score band
- **Regional concentration** — which regions carry the largest books and the highest default intensity
- **Loan purpose risk** — default behaviour compared across home, personal, car, business, and education loans
- **Financial drivers** — correlations between income, loan amount, interest rate, credit score, and debt-to-income ratio
- **Customer segmentation** — borrowers grouped into high, medium, and low risk categories

---

## License

Released under the MIT License. The dataset is synthetic and free to reuse.
