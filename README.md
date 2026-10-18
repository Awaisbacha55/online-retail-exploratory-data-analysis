# Online Retail Exploratory Data Analysis

### CodSoft Data Analytics Internship — Task 2

---

## Project Overview

This repository contains **Task 2: Exploratory Data Analysis (EDA)** completed as part of the **CodSoft Data Analytics Internship**. The project focuses on conducting an in-depth exploratory data analysis on the **Online Retail II** dataset, which comprises real-world transactional records from a UK-based online retail store.

The primary objective is to evaluate data quality, investigate transactional patterns, examine customer purchasing distributions, analyze product demand and geographic market contributions, identify statistical outliers, and provide evidence-backed answers to core business questions.

---

## CodSoft Internship Context

- **Internship Program:** CodSoft Data Analytics Internship
- **Task Number:** Task 2 — Exploratory Data Analysis (EDA)
- **Domain:** E-commerce Transaction Analytics / Retail Sales
- **Deliverable:** Fully documented Jupyter Notebook (`TASK_2_EXPLORATORY_DATA_ANALYSIS_(EDA).ipynb`) with embedded tables and visualizations

---

## Project Objectives

1. **Understand Dataset Architecture:** Inspect structure, schema, data types, and initial descriptive statistics across all features.
2. **Data Quality & Integrity Assessment:** Audit missing values, quantify null percentages, and detect exact duplicate rows.
3. **Data Preparation & Transformation:** Cast appropriate data types, filter out return transactions (negative quantities) and invalid unit prices, derive transactional line values (`LineValue = Quantity * Price`), and engineer monthly period stamps (`YearMonth`).
4. **Temporal Sales Analysis:** Aggregate and evaluate monthly revenue, unit sales volume, and transaction frequency across the observation period.
5. **Product & Market Performance:** Identify the highest-grossing products and determine the geographical revenue distribution across international markets.
6. **Distribution & Outlier Detection:** Analyze the statistical distribution of purchase quantities using Interquartile Range (IQR) fences.
7. **Bivariate Correlation Analysis:** Calculate and visualize linear correlations between numerical features (Quantity, Unit Price, and Line Value).
8. **Evidence-Based Business Synthesis:** Formulate concise, verified answers to strategic business questions based directly on computed outputs.

---

## Dataset Information

- **Dataset Name:** Online Retail II
- **Data Source:** [UCI Machine Learning Repository — Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- **Original File Format:** Microsoft Excel (`online_retail_II.xlsx`)
- **Analyzed Scope:** Sheet 1 (Transactional data from 01/12/2009 to 09/12/2010)
- **Total Initial Records:** 525,461 rows
- **Total Features:** 8 columns

### Attribute Summary

| Attribute | Data Type | Description |
| :--- | :--- | :--- |
| `Invoice` | Object / String | 6-digit transaction identifier; cancellations start with 'C' |
| `StockCode` | Object / String | 5-digit product code uniquely assigned to each distinct merchandise item |
| `Description` | Object / String | Product title or item description |
| `Quantity` | Integer (`int64`) | Quantities of each product ordered per transaction |
| `InvoiceDate` | Datetime (`datetime64[ns]`) | Timestamp of transaction generation |
| `Price` | Float (`float64`) | Product unit price in sterling (£) |
| `Customer ID` | Float (`float64`) | 5-digit unique identifier per customer |
| `Country` | Object / String | Country of customer residency |

---

## Technologies Used

- **Programming Language:** Python 3
- **Interactive Environment:** Google Colab / Jupyter Notebook
- **Core Data Libraries:**
  - **`pandas`** — DataFrame manipulation, temporal grouping, missing-value profiling, aggregations
  - **`numpy`** — Numerical operations and array handling
  - **`matplotlib.pyplot`** — Visual styling, figure configuration, layout formatting
  - **`seaborn`** — Statistical charting (time series line plots, categorical bar charts, histograms, heatmaps)
  - **`openpyxl`** — Excel workbook parsing engine

---

## Exploratory Data Analysis Methodology

The notebook is organized into a modular, step-by-step workflow:

1. **Environment Setup & Library Imports:** Configures Seaborn visualization styling (`whitegrid`) and global Matplotlib figure parameters (`10, 5`).
2. **Dataset Ingestion:** Ingests `online_retail_II.xlsx` into a Pandas DataFrame using the `openpyxl` engine.
3. **Descriptive Statistics & Schema Profiling:** Examines DataFrame dimensions (`525,461 x 8`), data types, non-null counts, and parametric summaries (mean, standard deviation, quartiles, min/max).
4. **Missing Value & Duplicate Audit:** Measures null counts per attribute, calculates missing percentages, checks for identical duplicate rows, and plots missing value counts.
5. **Data Preparation for Sales Analysis:**
   - Converts `InvoiceDate` to datetime objects.
   - Converts `Quantity` and `Price` to numeric types.
   - Calculates line transaction revenue: `LineValue = Quantity * Price`.
   - Filters transactions into a valid positive sales dataset (`Quantity > 0`, `Price > 0`, and non-null `InvoiceDate`).
   - Extracts monthly temporal markers (`YearMonth`).
6. **Monthly Trend Analysis:** Groups positive sales by `YearMonth` to compute aggregated revenue, total units sold, and unique transaction counts. Plots monthly revenue trajectory.
7. **Top Product Analysis:** Aggregates unit volume and revenue by product `Description`, sorts by gross revenue, and visualizes the top 10 products.
8. **Geographical Distribution:** Aggregates transactions by `Country` to measure national market share and visualizes the top 10 international markets.
9. **Quantity Distribution & Outlier Detection:** Plots a frequency distribution of purchase quantities and calculates IQR outlier boundaries ($Q1 - 1.5 \times IQR$ and $Q3 + 1.5 \times IQR$).
10. **Correlation Analysis:** Generates a Pearson correlation matrix across `Quantity`, `Price`, and `LineValue`, visualised via an annotated heatmap.
11. **Business Question Synthesis:** Directly extracts and reports the highest-earning month, top products, lead countries, valid transaction counts, and detected quantity outliers.

---

## Embedded Visualizations

All visual charts were generated and rendered directly within the Jupyter Notebook outputs:

1. **Missing Values by Column (Horizontal Bar Chart):** Compares missing value counts across all features, highlighting `Customer ID` and `Description`.
2. **Monthly Retail Revenue Trend (Line Plot with Markers):** Tracks revenue progression from December 2009 through December 2010.
3. **Top 10 Products by Positive Sales Revenue (Horizontal Bar Chart):** Ranks the top revenue-generating merchandise items.
4. **Top 10 Countries by Positive Sales Revenue (Horizontal Bar Chart):** Compares national sales volume, illustrating UK market concentration against export destinations.
5. **Distribution of Positive Transaction Quantities (Histogram):** Displays skewness and concentration of order quantities across 50 bins.
6. **Correlation Between Numerical Variables (Annotated Heatmap):** Quantifies linear associations between `Quantity`, `Price`, and `LineValue` with a diverging color map.

---

## Verified Key Findings

All figures below are extracted directly from the notebook outputs without alteration:

### 1. Dataset Dimensions & Quality
- **Total Initial Records:** 525,461 rows, 8 columns
- **Exact Duplicate Rows:** 6,865 rows
- **Missing Values:**
  - `Customer ID`: 107,927 missing entries (**20.54%** of dataset)
  - `Description`: 2,928 missing entries (**0.56%** of dataset)
  - All other fields (`Invoice`, `StockCode`, `Quantity`, `InvoiceDate`, `Price`, `Country`) contain **0%** missing values.

### 2. Transaction Segmentation
- **Negative-Quantity Records (Cancellations/Returns):** 12,326 records
- **Valid Positive-Sales Records:** 511,566 records used for sales, product, and country EDA

### 3. Monthly Sales & Seasonality Trends
- **Peak Revenue Month:** **November 2010 (`2010-11`)**
  - **Monthly Revenue:** £1,470,272.48
  - **Units Sold:** 728,449 units
  - **Transaction Count:** 2,747 unique transactions
- **Lowest Revenue Month:** February 2010 (`2010-02`) with £553,713.31 in revenue across 1,202 transactions.
- **Trend Observation:** Revenue showed steady growth from August 2010 onwards, surging sharply in October and November 2010 in anticipation of the holiday season.

### 4. Product Performance (Top 5 by Revenue)
| Rank | Product Description | Units Sold | Total Revenue (£) | Transactions |
| :---: | :--- | :---: | :---: | :---: |
| 1 | `Manual` | 2,831 | £262,992.08 | 516 |
| 2 | `REGENCY CAKESTAND 3 TIER` | 13,698 | £170,078.51 | 2,019 |
| 3 | `WHITE HANGING HEART T-LIGHT HOLDER` | 58,792 | £160,630.78 | 3,315 |
| 4 | `DOTCOM POSTAGE` | 730 | £116,408.71 | 730 |
| 5 | `ASSORTED COLOUR BIRD ORNAMENT` | 45,348 | £73,092.99 | 1,412 |

### 5. Geographic Market Contribution (Top 5 Countries)
| Rank | Country | Units Sold | Total Revenue (£) | Transactions |
| :---: | :--- | :---: | :---: | :---: |
| 1 | **United Kingdom** | 4,720,855 | £8,846,129.26 | 19,291 |
| 2 | **EIRE** | 193,116 | £380,977.82 | 348 |
| 3 | **Netherlands** | 183,616 | £268,786.00 | 135 |
| 4 | **Germany** | 108,722 | £202,395.32 | 347 |
| 5 | **France** | 163,183 | £147,211.49 | 241 |

*Note: The domestic UK market accounts for the overwhelming majority of total revenue and order volume.*

### 6. Quantity Outliers & Quartiles
- **Quartile 1 (Q1, 25th percentile):** 1.0 unit
- **Median (50th percentile):** 3.0 units
- **Quartile 3 (Q3, 75th percentile):** 10.0 units
- **Interquartile Range (IQR):** 9.0 units
- **Statistical Fences:**
  - Lower Bound: $-12.5$
  - Upper Bound: $23.5$
- **Detected Outliers:** **54,978** records exhibit order quantities above 23.5 units, representing wholesale or institutional customer purchases.

### 7. Correlation Analysis
| Feature | Quantity | Price | LineValue |
| :--- | :---: | :---: | :---: |
| **Quantity** | 1.000 | -0.005 | 0.325 |
| **Price** | -0.005 | 1.000 | 0.699 |
| **LineValue** | 0.325 | 0.699 | 1.000 |

- Unit `Price` exhibits a strong positive correlation with `LineValue` ($r \approx 0.70$).
- `Quantity` shows a moderate positive correlation with `LineValue` ($r \approx 0.33$).
- `Quantity` and `Price` exhibit practically zero linear correlation ($r \approx -0.01$).

---

## Repository Structure

```text
online-retail-exploratory-data-analysis/
├── .gitignore                                   # Excludes datasets, checkpoints, IDE, and cache files
├── LICENSE                                      # MIT License
├── README.md                                    # Comprehensive project documentation
├── requirements.txt                             # Python dependencies extracted from notebook
└── TASK_2_EXPLORATORY_DATA_ANALYSIS_(EDA).ipynb # Final exploratory analysis notebook with executed outputs
```

---

## Instructions for Opening and Running the Notebook

### Option A: Google Colab (Recommended)
1. Navigate to [Google Colab](https://colab.research.google.com/).
2. Click **File** > **Upload notebook** and select `TASK_2_EXPLORATORY_DATA_ANALYSIS_(EDA).ipynb`.
3. When prompted in Cell 6, upload your copy of `online_retail_II.xlsx`, or place it in the runtime filesystem under `/content/online_retail_II.xlsx`.
4. Run all cells sequentially from top to bottom.

### Option B: Local Jupyter Environment
1. Clone this repository:
   ```bash
   git clone https://github.com/Awaisbacha55/online-retail-exploratory-data-analysis.git
   cd online-retail-exploratory-data-analysis
   ```
2. (Optional) Create and activate a virtual environment:
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On macOS/Linux:
   source venv/bin/activate
   ```
3. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Download the dataset (`online_retail_II.xlsx`) from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii) and place it in the project root or update the `file_path` variable in Cell 6.
5. Launch Jupyter Notebook or JupyterLab:
   ```bash
   jupyter notebook
   ```
6. Open `TASK_2_EXPLORATORY_DATA_ANALYSIS_(EDA).ipynb` and view the existing outputs or execute the notebook.

---

## Dataset Download Instructions

Due to file size limitations on GitHub, the raw dataset (`online_retail_II.xlsx`, ~45 MB) is excluded from version control via `.gitignore`.

To acquire the original dataset:
1. Visit the official repository: [UCI Online Retail II Dataset (ID: 502)](https://archive.ics.uci.edu/dataset/502/online+retail+ii).
2. Download the compressed archive or `.xlsx` file.
3. Save `online_retail_II.xlsx` into your working directory or upload it when executing the notebook in Google Colab.

---

## Project Limitations

- **Cancellation Isolation:** Returns and cancellations (12,326 records with negative quantities) were separated from the positive sales dataset rather than paired against their original invoices to compute net sales per order.
- **Customer ID Sparsity:** 20.54% of transactions lack a `Customer ID`, reflecting guest checkouts. As a result, customer-level cohort and lifetime value analyses require imputation or separate treatment of unidentified transactions.
- **Observation Period:** The analysis covers the 2009–2010 transaction slice present in the first sheet of the dataset.

---

## Acknowledgments

- **CodSoft** for providing the Data Analytics Internship curriculum and practical real-world problem statements.
- **UCI Machine Learning Repository** and the original data providers for hosting the Online Retail II dataset.

---

## Author

- **Awais Bacha**
- **GitHub:** [@Awaisbacha55](https://github.com/Awaisbacha55)
- **Repository:** [online-retail-exploratory-data-analysis](https://github.com/Awaisbacha55/online-retail-exploratory-data-analysis)
