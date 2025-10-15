# E_commerce Transaction & Customer Behavior Analysis

This repository contains an exploratory data analysis notebook that investigates transactions and customer behavior from the "Online Retail II" dataset. The analysis covers data cleaning and multiple analyses including time-based revenue, customer segmentation (RFM), cohort retention, market-basket (association rules) analysis, and trend/seasonality decomposition.

## Contents

- `E_commerce_Transaction_&_Customer_Behavior_Analysis.ipynb` - Main Jupyter notebook with the full workflow and visualizations.

## Dataset

The notebook downloads and uses the "Online Retail II" dataset (commonly available on Kaggle). The code in the notebook uses `kagglehub` to fetch the dataset and reads the Excel file `online_retail_II.xlsx`.

Source (used programmatically in the notebook): lakshmi25npathi/online-retail-dataset

## What I did (high-level)

- Data ingestion: programmatically download and read the Excel file into a pandas DataFrame.
- Cleaning & preprocessing:
	- Drop rows with missing `Customer ID`.
	- Remove rows with non-positive `Quantity` values.
	- Parse `InvoiceDate` into datetime.
	- Add a `TotalPrice` column computed as `Quantity * Price`.
- Time-based analysis: aggregate daily revenue and plot revenue over time.
- Customer segmentation (RFM): compute Recency, Frequency, Monetary values per customer and create RFM segments and scores.
- Cohort analysis: compute monthly cohorts and plot retention heatmap.
- Market-basket / Association analysis: prepare invoice × item binary matrix and use `mlxtend` (`apriori`, `association_rules`) to find frequent itemsets and association rules.
- Trend & seasonality decomposition: decompose the daily revenue time series using `statsmodels`.

## Key files and notebook sections

- Data download & load: first notebook cells (uses `kagglehub` to download and read the Excel workbook).
- Preprocessing: dropping NA `Customer ID`, filtering `Quantity > 0`, converting dates, adding `TotalPrice`.
- Time-Based Analysis: computing `daily_rev` and plotting time series.
- RFM: grouping by `Customer ID` to compute Recency, Frequency, Monetary and scoring.
- Cohort Analysis: computing `CohortMonth`, `CohortIndex`, pivoting and plotting retention heatmap.
- Basket/Association Analysis: building `basket` (invoice × description) binary matrix and running `apriori` and `association_rules`.
- Trend/Seasonality: decomposing the daily revenue series and plotting components.

## Dependencies

The notebook installs or expects the following Python packages (the notebook includes some `%pip install` commands in cells):

- pandas
- numpy
- matplotlib
- seaborn
- kagglehub
- mlxtend
- statsmodels

You can create a virtual environment and install the packages manually. Example (PowerShell):

```powershell
# create and activate venv (Windows PowerShell)
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install pandas numpy matplotlib seaborn kagglehub mlxtend statsmodels
```

Note: The notebook uses `%pip install` in some cells which will install missing packages at runtime when executed in Jupyter.

## How to run

1. Open the notebook `E_commerce_Transaction_&_Customer_Behavior_Analysis.ipynb` in Jupyter or VS Code (Jupyter extension).
2. Make sure you have an internet connection (the notebook downloads the dataset with `kagglehub`).
3. Run cells from top to bottom. The download cell uses `kagglehub.dataset_download("lakshmi25npathi/online-retail-dataset")` and reads `online_retail_II.xlsx`.
4. If you want to limit memory usage, there is a cell which reads only the first 100,000 rows (`pd.read_excel(..., nrows=100000)`) — useful during development.

## Assumptions & notes

- The notebook assumes the Excel file contains sheets formatted like Online Retail II. If the file path or sheet names differ, update the path or `pd.read_excel` call.
- Some cells install packages at runtime using `%pip install`. If you prefer a reproducible environment use the commands in the Dependencies section to create a virtual env and install packages beforehand.
- The association rules section builds an invoice × product matrix using `Description`. Depending on the granularity you want, you may want to normalize or group similar product descriptions before analysis.

## Next steps / improvements

- Improve product description cleaning (normalize strings, remove stopwords, group similar SKUs).
- Use transactional-level support thresholds adjusted per dataset size for the `apriori` step.
- Add more visualizations and interactive dashboards (Plotly, Dash, or Streamlit).
- Persist cleaned data to disk (CSV/Parquet) to avoid re-downloading and reprocessing during iterative development.

## Contact

If you want to collaborate or need clarification, open an issue or contact the repository owner.

---

README last updated: October 2025
