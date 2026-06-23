# Marketing Campaign Data Analysis

A data cleaning and feature engineering project built on a real-world marketing campaign dataset. The goal is to prepare raw customer data for downstream analysis and visualization by handling missing values, fixing data types, engineering useful features, and detecting outliers.

---

## Project Structure

```
marketing-campaign-project/
│
├── Marketing_Campaign_project.ipynb   # Main analysis notebook
├── marketing_campaign.xlsx            # Raw input dataset
└── marketing_campaign_cleaned_data.csv  # Exported cleaned dataset
```

---

## Project Objectives

- Load and explore raw marketing campaign data
- Handle missing values and fix incorrect data types
- Engineer new features to enrich the dataset
- Detect outliers using the IQR (Interquartile Range) method
- Export a clean dataset ready for visualization and further analysis

---

## Dataset Overview

The dataset contains customer-level data including demographics, product spending, campaign responses, and purchase channel behavior.

**Key columns include:**
- `Income` — Annual customer income
- `Dt_Customer` — Date of customer enrollment
- `MntWines`, `MntFruits`, `MntMeatProducts`, `MntFishProducts`, `MntSweetProducts`, `MntGoldProds` — Amount spent per product category
- `NumWebPurchases`, `NumStorePurchases`, `NumCatalogPurchases` — Purchase channel counts
- `AcceptedCmp1–5` — Whether campaigns 1–5 were accepted (binary: 0/1)
- `Z_Revenue`, `Z_CostContact` — Revenue and cost per contact
- `Education`, `Marital_Status` — Customer demographic attributes

---

## Data Cleaning Steps

| Step | Action |
|------|--------|
| Null value check | `Income` had 24 missing values → filled with **median** |
| Duplicate check | No duplicate rows found |
| Data type fix | `Dt_Customer` converted from `object` → `datetime` |

---

## Feature Engineering

Three new features were created to enrich the dataset:

| Feature | Formula |
|---------|---------|
| `Total Spend` | Sum of all product spending columns |
| `Total Purchases` | Sum of web + store + catalog purchases |
| `ROI` | `((Z_Revenue - Z_CostContact) / Z_CostContact) * 100` |

---

## Outlier Detection

Outliers were identified using the **IQR (Box Plot) method**:

```
Lower Fence = Q1 - 1.5 × IQR
Upper Fence = Q3 + 1.5 × IQR
```

**Note:** Columns `AcceptedCmp1–5` are binary (0/1) flags and were intentionally excluded from outlier treatment, as their distribution is expected to be skewed.

Outlier treatment options considered:
- Capping (Winsorization)
- Dropping outlier rows
- Replacing with mean/median *(commented out — preserved for optional use)*

---

## Dashboard Visualizations (Power BI)

After cleaning, the dataset was analyzed in Power BI. Key charts include:

- **Count of ID by Education** — Majority of customers hold a Graduation degree (50.31%)
- **Spending by Product Category** — Wines dominate at 50.17% of total spend
- **Count of ID by Marital Status** — Married customers are the largest segment (38.57%)
- **Total Conversions vs Total Leads** — Equal 50/50 split between conversions and leads
- **Campaign Acceptance (Cmp1–5)** — Grouped bar chart showing acceptance rates across all 5 campaigns

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Data processing |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Google Colab | Development environment |
| Google Drive | File storage |
| Power BI | Dashboard and visualization |

---

## How to Run

1. Upload `marketing_campaign.xlsx` to your Google Drive.
2. Open `Marketing_Campaign_project.ipynb` in Google Colab.
3. Mount your Google Drive and update the file path if needed.
4. Run all cells in order.
5. The cleaned CSV will be saved to your Drive as `marketing_campaign_cleaned_data.csv`.

---

## Key Insights

- Over **50%** of customers are graduates, suggesting an educated customer base.
- **Wines** account for the largest share of spending, making it the top product category.
- Campaign acceptance rates vary — further analysis can identify the most effective campaign.
- The equal conversion-to-lead ratio indicates room to improve campaign conversion strategies.
