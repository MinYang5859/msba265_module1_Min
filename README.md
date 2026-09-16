# MSBA 265 Module 1: Exploratory Data Analysis

## Project Overview

This project completes the Module 1 exploratory data analysis and production outlier-filtering workflow for the French Motor Third Party Liability Claims dataset from OpenML. The dataset contains 678,013 policy records and 12 variables.

The project includes:

- Programmatic data collection
- Raw boundary and missing-value audits
- A Business Data Dictionary
- Skewness and domain-based transformation analysis
- Pearson correlation analysis
- Distribution and outlier visualizations
- Tukey IQR and Z-score comparison
- A reusable production outlier-filtering script
- A compiled final PDF report

## Project Structure

```text
msba265_module1/
├── .gitignore
├── README.md
├── requirements.txt
├── Module1_Homework_Report.pdf
├── data/
│   ├── download_data.py
│   ├── raw_business_data.csv
│   └── cleaned_business_data.csv
├── notebooks/
│   └── 01_eda_and_data_dictionary.ipynb
├── src/
│   └── clean_outliers.py
└── reports/
    ├── data_dictionary.csv
    └── figures/
        ├── correlation_heatmap.png
        ├── feature_distributions.png
        └── outlier_filtering_comparison.png
```

## Reproduction Instructions

The following instructions are written for Visual Studio Code on Windows. Run all commands from the project root directory.

### 1. Clone the GitHub repository

```cmd
git clone https://github.com/MinYang5859/msba265_module1_Min.git
cd msba265_module1_Min
```

### 2. Create a virtual environment

```cmd
python -m venv venv
```

### 3. Activate the virtual environment

For Windows Command Prompt:

```cmd
venv\Scripts\activate
```

For Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

### 4. Install the required packages

```cmd
python -m pip install -r requirements.txt
```

### 5. Download the raw dataset

```cmd
python data\download_data.py
```

Expected output:

```text
data/raw_business_data.csv
678,013 rows x 12 columns
```

### 6. Run the Jupyter Notebook

Open the following file in Visual Studio Code:

```text
notebooks/01_eda_and_data_dictionary.ipynb
```

Select the Python interpreter from the project virtual environment:

```text
venv\Scripts\python.exe
```

Then select:

```text
Restart Kernel and Run All Cells
```

The Notebook generates:

```text
reports/data_dictionary.csv
reports/figures/correlation_heatmap.png
reports/figures/feature_distributions.png
reports/figures/outlier_filtering_comparison.png
```

### 7. Run the production outlier-filtering script

```cmd
python src\clean_outliers.py
```

Expected results:

```text
Initial records: 678,013
Tukey IQR valid range: -2,257 to 4,007
Removed records: 77,566
Final cleaned records: 600,447
```

The script generates:

```text
data/cleaned_business_data.csv
```

### 8. Open the final report

The compiled assignment report is available in the repository root:

```text
Module1_Homework_Report.pdf
```

## Main Findings

- All 12 variables contain 678,013 non-null observations.
- `DrivAge` ranges from 18 to 100 with no negative-age records.
- `Exposure` ranges from 0.002732 to 2.01 with no zero or negative values.
- `BonusMalus` ranges from 50 to 230.
- Common numeric sentinel codes were not detected in the audited variables.
- `ClaimNb` has a skewness coefficient of approximately 5.60, and 94.98% of records contain zero claims.
- `ClaimNb` remains in raw count units because `log(0)` is undefined and count-based models better preserve its business meaning.
- No numerical feature pair reaches the severe Pearson correlation threshold of `|r| ≥ 0.85`.
- `Density` is strongly right-skewed, with a median of 393 and a maximum of 27,000.
- Tukey filtering flags 77,566 `Density` records, while the Z-score method flags 15,209.
- Statistical outliers should not be treated automatically as data errors because high-density observations may represent valid urban policyholders.

## Reproducible Artifacts

| Artifact | Location |
|---|---|
| Raw dataset | `data/raw_business_data.csv` |
| Cleaned dataset | `data/cleaned_business_data.csv` |
| Business Data Dictionary | `reports/data_dictionary.csv` |
| Correlation heatmap | `reports/figures/correlation_heatmap.png` |
| Distribution charts | `reports/figures/feature_distributions.png` |
| Outlier comparison | `reports/figures/outlier_filtering_comparison.png` |
| Final report | `Module1_Homework_Report.pdf` |

## Peer Replication

Before final submission, a classmate will clone this public repository and follow the instructions above without additional assistance. A peer replication statement will be added to the repository after the reproduction test is completed.

## Author

Min Yang  
MSBA 265 – Special Analytics Topics