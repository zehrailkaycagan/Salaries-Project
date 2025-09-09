# Salaries Project

A concise exploratory data analysis (EDA) of a public employee salary dataset using Jupyter Notebook. The analysis in `salaries.ipynb` covers data loading, cleaning, descriptive statistics, and targeted queries to surface actionable insights.

## Table of Contents
- Overview
- Dataset
- Analysis Scope
- Key Findings
- How to Run
- Project Structure

## Overview
The goal is to quickly understand the structure and quality of the salary data, resolve type and missing-value issues, and answer common business questions (e.g., pay distributions by year and job title, highest base pay records, and frequent roles).

The notebook runs on Python 3.10 and primarily uses `pandas` and `numpy`.

## Dataset
- Source file: `Salaries` (CSV)
- Core columns: `Id, EmployeeName, JobTitle, BasePay, OvertimePay, OtherPay, Benefits, TotalPay, TotalPayBenefits, Year, Notes, Agency, Status`
- Initial size: 148,654 rows × 13 columns

Notes:
- `Notes` is entirely empty (all values missing)
- `Benefits` and `Status` contain a high proportion of missing values

## Analysis Scope
Key activities performed in the notebook:
- Data ingestion and preview (first/last records)
- Dimensional and type summaries: `data.shape`, `data.info()`, `data.describe(include='all')`
- Missing value analysis: `data.isnull().sum()` and row-level NaN counts
- Feature reduction: Dropped `['Id','Notes','Agency','Status']` (reduced to 9 columns)
- Text queries/filters:
  - Title filters with `.str.contains('CAPTAIN', case=False)` and `.str.contains('fire', case=False)`
  - Frequency analyses via `value_counts()` on employee names and job titles
- Type conversion and cleaning:
  - `BasePay` coerced to numeric (`pd.to_numeric(..., errors='coerce')`)
  - Rows with NaN in `BasePay` removed
- Descriptive statistics and grouping:
  - Mean `BasePay` by year: `groupby('Year').mean()['BasePay']`
  - Mean `BasePay` by job title: `groupby('JobTitle').mean()['BasePay']`
- Specific lookups:
  - Record with maximum `BasePay`
  - For `ALBERT PARDINI`, retrieved `JobTitle` and `TotalPayBenefits`

## Key Findings
- Distinct job titles: 2,159
- Most frequent employee name: Kevin Lee (13 occurrences)
- Records with job titles containing "CAPTAIN": 552
- Employees with job titles containing "fire": 5,879
- Average BasePay by year (USD):
  - 2011: 63,595.96
  - 2012: 65,436.41
  - 2013: 69,630.03
  - 2014: 66,564.42
- Highest BasePay: Gregory P Suhr (Chief of Police), BasePay = 319,275.01 (2013)
- Most common job title: Transit Operator (6,975 records)

## How to Run
Prerequisites:
- Python 3.10+
- Jupyter Notebook or JupyterLab

Required packages:
- pandas
- numpy

Setup and execution:
```bash
# (Optional) create and activate a virtual environment
python -m venv .venv && .\.venv\Scripts\activate

# Install dependencies
pip install pandas numpy jupyter

# Launch the notebook
jupyter notebook salaries.ipynb
```

Ensure the data file `Salaries` (CSV) exists in the project root, or update the path in `pd.read_csv('Salaries')` accordingly.

## Project Structure
```
Salaries-Project/
├─ Salaries                 # Data file (CSV)
├─ salaries.ipynb          # Analysis notebook
└─ README.md               # This file
```
