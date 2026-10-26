# Home Credit Default Risk — Exploratory Data Analysis (EDA)

## Project Overview

This project explores the **Home Credit Default Risk** application data to understand applicant characteristics, missing data, and how features differ between applicants who experienced payment difficulties and those who did not.

The analysis is implemented in a Jupyter Notebook using Python and common data-analysis and visualization libraries. It is an exploratory analysis project; it does **not** build or validate a predictive credit-risk model.

## Business Problem

Lenders need to understand the characteristics of loan applicants and the quality of the data available to assess repayment risk. This notebook investigates the application dataset, examines missing values, and compares the `TARGET` groups.

In the dataset used here:

- `TARGET = 1` represents a client with payment difficulties.
- `TARGET = 0` represents a client without the recorded payment-difficulty outcome.

These are exploratory comparisons, not evidence that any feature causes default.

## Dataset

The notebook reads two CSV files:

- `application_data.csv` — applicant-level application information.
- `previous_application.csv` — information about previous loan applications.

The notebook originally loads these files from Google Drive paths. To run it locally, download the matching files from the **Home Credit Default Risk** competition dataset on Kaggle and update the paths in the notebook.

**Dataset source:** [Home Credit Default Risk — Kaggle](https://www.kaggle.com/competitions/home-credit-default-risk/data)

The raw datasets are not included in this repository. Please follow the dataset's terms and Kaggle's rules when downloading or sharing data.

### Dataset dimensions recorded in the notebook

- `application_data.csv`: **307,511 rows and 122 columns** before the notebook's column filtering.
- After removing columns with at least 50% missing values, the application data has **307,511 rows and 81 columns**.
- `previous_application.csv`: **1,670,214 rows and 37 columns**.
- The inner join on `SK_ID_CURR` produces **1,413,701 rows** in the notebook.

These figures reflect the notebook's recorded outputs and may change if a different dataset version is used.

## Tools and Libraries

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook / Google Colab

## Work Performed

### 1. Initial data inspection
- Loaded the application dataset.
- Inspected sample records, dimensions, columns, descriptive statistics, and non-null counts.
- Separated numeric and categorical columns for exploration.

### 2. Missing-value analysis
- Calculated missing-value counts and percentages.
- Removed application-data columns with 50% or more missing values.
- Examined distributions for selected numeric features using descriptive statistics and histograms.
- Tried filling missing values using mode, median, mean, or other replacement logic depending on the column.

### 3. Target-group exploration
- Split applicants into `TARGET = 0` and `TARGET = 1` groups.
- Compared categorical distributions using plots.
- Created correlation heatmaps for numeric/encoded features.
- Compared numerical feature distributions between target groups using histograms.
- Plotted numeric columns to inspect possible outliers.

### 4. Previous-application exploration
- Loaded the previous-application dataset.
- Inspected its dimensions and application identifiers.
- Joined it to the main application data using `SK_ID_CURR`.
- Started exploring previous application status alongside applicant education and contract-status fields.

## Preliminary Observations

The recorded notebook outputs show:

- The original application table contains **307,511 applicants**.
- After the 50%-missingness filter, **81 columns** remain.
- The notebook output counts **24,825** records with `TARGET = 1` and **282,686** with `TARGET = 0`.
- The notebook's recorded ratio of `TARGET = 1` to `TARGET = 0` is approximately **0.0878**.
- Several columns have substantial missingness; for example, `FLOORSMAX_AVG`, `FLOORSMAX_MODE`, and `FLOORSMAX_MEDI` each show approximately **49.76%** missing values in the recorded output.

These are descriptive results from the notebook's saved outputs, not independently re-run or validated results.

## How to Run

1. Clone or download this repository.
2. Download the required CSV files from the Kaggle competition page.
3. Place the files in a local data folder, or mount Google Drive if using Google Colab.
4. Update the two `pd.read_csv(...)` paths in the notebook:
   - `application_data.csv`
   - `previous_application.csv`
5. Install the required libraries if they are not already available:

   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

6. Open `EDA_assignment.ipynb` in Jupyter Notebook or Google Colab.
7. Run the cells in order and review the outputs.

## Important Validation Notes

This notebook is a work in progress and should be reviewed before its results are used for business decisions or presented as a fully validated analysis:

- Missing-value treatments are not consistently applied. Some columns are filled using mean, median, or mode, and the choice should be checked against each feature's data type and distribution.
- The `OCCUPATION_TYPE` treatment appears to use a numeric income value to fill a categorical field. This should be corrected before analysis.
- The `EMERGENCYSTATE_MODE` missing-value treatment should be reviewed; the current code uses a null count as the replacement value.
- One `EXT_SOURCE_2` treatment references `AMT_GOODS_PRICE` value counts. This appears inconsistent with the target column and should be checked.
- The merge with `previous_application.csv` is performed on `SK_ID_CURR`. Because a customer can have multiple previous applications, the result contains repeated customer-level rows. Any subsequent applicant-level counts or comparisons must account for this one-to-many relationship.
- The notebook contains a possible typo (`aapp`) and some deprecated plotting patterns; run the notebook from top to bottom and resolve errors in the target environment.
- The analysis explores correlations and group differences. It does not establish causation, and no model performance has been measured.

## Suggested Next Improvements

- Correct and document missing-value strategies by data type.
- Keep a record of row/column counts before and after cleaning.
- Validate duplicates and join cardinality before merging.
- Compare target rates across selected categorical and numeric features.
- Summarize key findings with clearly labelled plots and concise business interpretations.
- Add a reproducible environment file and a final conclusion after the notebook is validated.

## Repository Contents

```text
home-credit-default-risk-eda/
├── README.md
└── EDA_assignment.ipynb
```

## Author

**Krishna**  
Data Analytics Portfolio Project

---

*This repository documents exploratory work contained in the notebook. Findings and data-cleaning steps should be validated before being described as final business conclusions.*
