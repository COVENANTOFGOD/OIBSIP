
## Project Overview

This project demonstrates a professional data-cleaning workflow using Python, pandas, and NumPy.

The objective was to take a deliberately messy cafe sales dataset and systematically transform it into a clean, analysis-ready dataset.

The project focuses on identifying data-quality problems, documenting cleaning decisions, correcting inconsistencies, 
detecting outliers, and validating the dataset after cleaning.
<img width="1365" height="685" alt="Screenshot 2026-10-08 074011" src="https://github.com/user-attachments/assets/a263287f-05d2-4d97-ab8c-c8439ef069db" />

---

## Business Problem

Raw business data often contains missing values, duplicate records, inconsistent formatting, incorrect data types, and invalid values.

Before the data can be used for reporting, dashboards, or business analysis, these quality issues must be identified and addressed.

This project answers the following question:

> **How can a messy transactional dataset be transformed into a reliable dataset suitable for analysis?**

---

## Dataset

**Dataset:** Cafe Sales — Dirty Data for Cleaning Training

**Source:** Kaggle

The dataset contains cafe transaction records with deliberately introduced data-quality issues.

### Dataset Features

| Column           | Description                            |
| ---------------- | -------------------------------------- |
| Transaction ID   | Unique identifier for each transaction |
| Item             | Product purchased                      |
| Quantity         | Number of items purchased              |
| Price Per Unit   | Price of one unit                      |
| Total Spent      | Total transaction amount               |
| Payment Method   | Method used for payment                |
| Location         | Transaction location                   |
| Transaction Date | Date of transaction                    |

The original dataset contains **10,000 transaction records and 8 columns**.
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/e46cb2fe-6119-46dc-b581-1b4e2c7814fc" />

---

## Tools & Technologies

- Python
- pandas
- NumPy
- Jupyter Notebook

### Python Libraries

```python
import pandas as pd
import numpy as np
```
<img width="1365" height="685" alt="Screenshot 2026-10-08 074011" src="https://github.com/user-attachments/assets/fa34af02-21ba-4b53-8e60-ad31586349da" />

---

## Data Quality Issues Identified

The initial investigation identified several data-quality problems:

- Missing values
- `UNKNOWN` values
- `ERROR` values
- Duplicate records
- Incorrect data types
- Numeric values stored as text
- Transaction dates stored as text
- Potential statistical outliers
- Inconsistent categorical formatting

Initially, all eight columns were stored as `object` dtype, including columns that should have been numeric or datetime.
<img width="1365" height="690" alt="Screenshot 2026-10-08 074028" src="https://github.com/user-attachments/assets/e2c6dcf3-937e-4bcd-aca5-626acc4b0ca3" />

---

## Data Cleaning Process

### 1. Data Quality Assessment

A baseline quality report was created before cleaning.

The assessment included:

- Number of rows and columns
- Missing values
- Missing-value percentages
- Duplicate records
- Unique values
- Data types
- Numerical ranges

This established the **before-cleaning state** of the dataset.

---

### 2. Missing Data Handling

Invalid values such as:

```text
UNKNOWN
ERROR
```

were converted to missing values.

Different strategies were then applied depending on the column.

| Column Type      | Strategy               | Reason                                                          |
| ---------------- | ---------------------- | --------------------------------------------------------------- |
| Quantity         | Median imputation      | Numeric variable and median is less sensitive to extreme values |
| Price Per Unit   | Median imputation      | Numeric variable                                                |
| Total Spent      | Median imputation      | Numeric variable                                                |
| Item             | Mode imputation        | Categorical variable                                            |
| Payment Method   | Mode imputation        | Categorical variable                                            |
| Location         | Mode imputation        | Categorical variable                                            |
| Transaction Date | Missing values removed | Dates should not be artificially inferred                       |

The goal was to preserve as much valid transaction information as possible while avoiding inappropriate assumptions.

---

### 3. Duplicate Removal

Exact duplicate rows were identified using:

```python
df.duplicated()
```

Duplicate records were removed using:

```python
df.drop_duplicates()
```

The number of duplicates removed was documented in the notebook.

---

### 4. Data Standardisation

Text fields were standardised by removing unnecessary whitespace and applying consistent capitalization.

For example:

```python
df["Payment Method"] = df["Payment Method"].str.title()
df["Location"] = df["Location"].str.title()
```
<img width="1365" height="687" alt="Screenshot 2026-10-08 074124" src="https://github.com/user-attachments/assets/dd1d46e5-1422-489f-b406-cfe79a13dab5" />

Transaction dates were converted from text to pandas datetime format.

---
<img width="1363" height="687" alt="Screenshot 2026-10-08 074045" src="https://github.com/user-attachments/assets/6c0a809a-cb6a-49b9-ae96-adcfe75b402d" />

### 5. Outlier Detection

The **Interquartile Range (IQR)** method was used to identify potential outliers in numeric columns.

The method uses:

```text
IQR = Q3 - Q1
```

Potential outliers were identified using the lower and upper IQR boundaries.

Outliers were **retained when they represented potentially legitimate transactions**, rather than automatically deleting them.

This prevents legitimate high-value transactions from being incorrectly classified as data errors.

---

### 6. Data Type Correction

The final dataset was converted to appropriate data types.

| Column           | Final Type |
| ---------------- | ---------- |
| Transaction ID   | string     |
| Item             | string     |
| Quantity         | Int64      |
| Price Per Unit   | float64    |
| Total Spent      | float64    |
| Payment Method   | string     |
| Location         | string     |
| Transaction Date | datetime64 |

Correct data types improve reliability and make the dataset suitable for downstream analysis.

---

## Validation

After cleaning, the dataset was validated using:

- Final row count
- Final null count
- Final duplicate count
- Final data types
- Final dataset structure

A **before-vs-after summary table** was also produced to measure the effect of the cleaning process.

### Validation Framework

```text
Raw Dataset
     ↓
Data Quality Assessment
     ↓
Cleaning & Standardisation
     ↓
Outlier Detection
     ↓
Data Type Correction
     ↓
Validation
     ↓
Clean Dataset
```

---

## Output

The cleaned dataset was exported as:

```text
cleaned_cafe_sales.csv
```

The cleaned file is ready for further analysis, visualization, dashboard development, or statistical modelling.
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/dc89be35-ef3f-45cb-8fa1-90794329b0c6" />

---

## Project Structure

```text
Task-3-Data-Cleaning/
│
├── dirty_cafe_sales.csv
│
├── cleaned_cafe_sales.csv
│
├── Task_3_Data_Cleaning.ipynb
│
├── README.md

```

---

## Key Skills Demonstrated

This project demonstrates practical skills in:

- Data profiling
- Data quality assessment
- Missing-value handling
- Duplicate detection
- Data standardisation
- Outlier detection
- Data type conversion
- Data validation
- pandas
- NumPy
- Jupyter Notebook
- Documentation of analytical decisions

---

## Key Takeaway

Data cleaning is not simply about removing nulls and duplicates.

A professional cleaning process requires understanding **what the data represents**, identifying the cause and impact of quality problems, selecting an appropriate treatment, and validating the result.

This project demonstrates that process from **raw data → cleaned data → validated dataset**.

---

## Author

**Irogementi Covenant**

Business Analyst | Data Analyst

### Core Skills

`Python` · `SQL` · `Excel` · `Power BI` · `Tableau`
