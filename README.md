# Logistics Data Cleaning and Exploratory Data Analysis (EDA)

## Project Overview
This project performs data cleaning and exploratory data analysis (EDA) on the **DataCo Smart Supply Chain for Big Data Analysis** dataset from Kaggle. The goal is to prepare logistics data for analysis, identify data-quality issues, and explore patterns related to shipping time, delivery performance, sales, and other supply-chain measures.

**Dataset source:** [DataCo Smart Supply Chain for Big Data Analysis — Kaggle](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)

> **Note:** The dataset is not included in this repository. Download it from Kaggle and place the main CSV file in the project folder before running the notebook.

## Project Objectives
- Inspect the dataset structure, data types, descriptive statistics, missing values, and duplicate records.
- Standardize column names and remove exact duplicate rows.
- Convert available date and numeric columns to appropriate data types.
- Handle missing values with simple, documented rules.
- Detect and cap selected numeric outliers using the Interquartile Range (IQR) method.
- Explore shipping time, delivery delays, shipping modes, sales patterns, and correlations.
- Export the cleaned dataset and data-quality summaries.

## Tools and Libraries
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Repository Files
```text
.
├── Logistics_Data_Cleaning_EDA.ipynb
├── Logistics_Data_Cleaning_EDA_Report.docx
└── README.md
```

After running the notebook, it also creates:
- `dataco_cleaned.csv` — cleaned dataset
- `missing_value_summary.csv` — missing-value counts before and after cleaning
- `outlier_summary.csv` — IQR bounds and outlier counts for selected numeric columns

## Getting Started

### 1. Download the dataset
1. Open the [Kaggle dataset page](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis).
2. Sign in to Kaggle if prompted.
3. Download and extract the dataset.
4. Place `DataCoSupplyChainDataset.csv` in the same folder as the notebook.

If your downloaded CSV has a different filename, update `FILE_PATH` near the beginning of the notebook.

### 2. Set up Python
Python 3.10 or later is recommended.

Create and activate a virtual environment from the project folder.

**Windows PowerShell**
```powershell
python -m venv .venv
.\\.venv\\Scripts\\Activate.ps1
python -m pip install --upgrade pip
pip install pandas numpy matplotlib seaborn jupyter
```

**macOS / Linux**
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install pandas numpy matplotlib seaborn jupyter
```

### 3. Run the notebook
Start Jupyter:
```bash
jupyter notebook
```

Open `Logistics_Data_Cleaning_EDA.ipynb` and run the cells from top to bottom. You can also open and run the notebook in Visual Studio Code with the Jupyter extension installed.

## Data Cleaning Workflow
1. **Initial inspection:** Check the number of rows and columns, data types, descriptive statistics, missing values, and exact duplicates.
2. **Column-name standardization:** Convert column names to lowercase and replace spaces/special characters with underscores.
3. **Duplicate removal:** Remove exact duplicate rows.
4. **Data-type conversion:** Parse columns with date-like names as dates and convert common numeric measures when present.
5. **Missing-value handling:**
   - Numeric columns: fill missing values with the median.
   - Categorical/text columns: fill with the mode, or `Unknown` if no mode exists.
   - Date columns: leave invalid or missing dates unresolved rather than guessing dates.
6. **Outlier treatment:** Use the IQR rule to identify outliers in selected numeric measures and cap them at the calculated lower/upper bounds.
7. **Feature creation:** When available, calculate `delivery_delay_days` as actual shipping days minus scheduled shipping days, and create a late-delivery flag.
8. **Export:** Save the cleaned dataset and quality summaries to CSV files.

> **Important:** Outlier capping changes values and is a modelling choice, not proof that an extreme observation is incorrect. Keep the raw dataset and compare results before and after capping.

## Exploratory Data Analysis
The notebook creates the following outputs when the required columns are present:
- Missing-value percentage bar chart
- Histograms of selected sales, shipping-time, and quantity measures
- Scatter plot of actual versus scheduled shipping time
- Shipping-mode summary for the available late-delivery indicator or derived delay flag
- Sales by region, market, or country
- Correlation heatmap for selected numeric measures
- Descriptive statistics and a data-quality summary

Plots are skipped with a message if the relevant columns are not present in the downloaded dataset version.

## Understanding Delivery Delay
When actual and scheduled shipping-day fields are available:

`delivery_delay_days = actual_shipping_days - scheduled_shipping_days`

- Positive value: delivery took longer than scheduled.
- Zero: actual duration matched the schedule.
- Negative value: delivery took less time than scheduled.

Check the dataset's data dictionary before interpreting `late_delivery_risk`: it may be a pre-defined indicator or label rather than an observed delivery outcome.

## Outputs and Report
The notebook exports:
- `dataco_cleaned.csv`
- `missing_value_summary.csv`
- `outlier_summary.csv`

The Word report (`Logistics_Data_Cleaning_EDA_Report.docx`) documents the objectives, tools, cleaning methodology, EDA methods, limitations, recommendations, and a results table to complete using the actual notebook output.

## Limitations
- The dataset is simulated and may not reflect all real-world logistics operations.
- Missing-value imputation can reduce variation and may hide patterns in why values are missing.
- IQR outlier capping can affect summary statistics; compare capped and uncapped data.
- Rows may represent order items rather than unique shipments or orders. Confirm the dataset's grain before reporting operational totals.
- Avoid publishing raw customer identifiers or personal information.

## Future Improvements
- Investigate missingness by region, shipping mode, and other relevant groups.
- Compare delivery performance across time periods and geographic segments.
- Build a Power BI dashboard for sales, delivery delay, and shipping-mode KPIs.
- Use time-based validation if building forecasting models.
- Maintain a data dictionary and document any additional business rules.

## Author
Add your name, GitHub profile, and project date here.

## License and Dataset Attribution
This project uses the publicly available DataCo dataset for educational analysis. Review the Kaggle dataset page and its terms/license before redistributing the data or derived files. The dataset itself is not included in this repository.
