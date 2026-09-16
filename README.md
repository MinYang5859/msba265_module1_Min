# MSBA 265 Module 1: Exploratory Data Analysis

## Project Overview

This project completes the Module 1 exploratory data analysis workflow for an automobile insurance dataset containing 678,013 policy records.

The project includes:

* Programmatic data collection
* Data quality auditing
* A business data dictionary
* Skewness analysis
* Correlation analysis
* Distribution and outlier visualization
* Tukey IQR and Z-score outlier comparison
* A reusable production outlier-filtering script

## Project Structure

```text
msba265_module1/
├── .gitignore
├── README.md
├── requirements.txt
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

The raw and cleaned CSV files are generated locally and excluded from Git through `.gitignore`.

## Environment Setup

This project was developed in Visual Studio Code on Windows using Python and a virtual environment.

### 1. Create the virtual environment

Open the VS Code Terminal in the project root directory and run:

```cmd
python -m venv venv
```

### 2. Activate the virtual environment

For Windows Command Prompt:

```cmd
venv\Scripts\activate
```

For Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

### 3. Install the required packages

```cmd
pip install -r requirements.txt
```

## How to Run the Project

All commands should be executed from the project root directory.

### Step 1: Download the raw dataset

```cmd
python data/download_data.py
```

This command creates:

```text
data/raw_business_data.csv
```

### Step 2: Run the Jupyter Notebook

Open the following file in VS Code:

```text
notebooks/01_eda_and_data_dictionary.ipynb
```

Select the correct Python kernel and choose:

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

### Step 3: Run the production outlier-filtering script

```cmd
python src/clean_outliers.py
```

This command creates:

```text
data/cleaned_business_data.csv
```

## Main Findings

The dataset contains 678,013 policy records and 12 variables.

The data quality audit found no standard null values. However, variable definitions and numerical ranges were also reviewed because non-null values can still contain invalid or sentinel values.

The correlation audit did not identify any severe pairwise correlation at the selected threshold of absolute Pearson correlation greater than or equal to 0.85.

The `Density` feature is strongly right-skewed. Its observed statistics are:

```text
Q1: 92
Median: 393
Q3: 1,658
Mean: 1,792.42
Standard deviation: 3,958.65
Maximum: 27,000
```

The Tukey IQR valid range for `Density` is:

```text
-2,257 to 4,007 people per square kilometer
```

The comparison produced the following results:

```text
Tukey IQR records flagged: 77,566 (11.44%)
Z-score records flagged:   15,209 (2.24%)
```

The difference occurs because the extreme right tail increases the mean and standard deviation, making the Z-score method less sensitive to high-density observations.

Statistical outliers are not automatically data errors. High-density observations may represent valid urban policyholders. Removing all of them could introduce geographic selection bias. A `log1p(Density)` transformation should therefore be considered when the modeling objective requires retaining valid urban records.

## Reproducibility

The project uses:

* `requirements.txt` to record package dependencies
* `.gitignore` to exclude the virtual environment, checkpoints, and generated datasets
* Python scripts to reproduce data collection and filtering
* A Jupyter Notebook to reproduce the exploratory analysis and visual outputs

## Author

Min Yang
MSBA 265 – Special Analytics Topics
