# Marketing Campaign Data Cleaning Project

## Overview
This project performs data cleaning and preprocessing on a marketing campaign dataset to prepare it for analysis. The cleaned dataset is ready for exploratory data analysis (EDA) and machine learning modeling.

## Dataset Information
- **Original File**: `marketing_campaign.csv`
- **Cleaned File**: `marketing_campaign_cleaned.xlsx`
- **Original Records**: 2,240 rows × 29 columns
- **Cleaned Records**: 2,240 rows × 28 columns

## Data Cleaning Steps

### 1. Missing Value Handling
- Identified 24 missing values in the `Income` column
- Removed the entire `Income` column due to missing data
- Verified no other missing values exist in remaining columns

### 2. Duplicate Removal
- Checked for duplicate rows using `.drop_duplicates()`
- No duplicate records found in the dataset
- All 2,240 records are unique

### 3. Column Renaming
Standardized all column names to lowercase with underscores for consistency:

| Original Column | Renamed Column |
|----------------|----------------|
| ID | id |
| Year_Birth | year_birth |
| Education | education |
| Marital_Status | marital_status |
| Kidhome | kids_home |
| Teenhome | teens_home |
| Dt_Customer | customer_date |
| MntWines | amount_wines |
| AcceptedCmp3 | accepted_campaign_3 |
| ... | ... |

### 4. Text Value Standardization

#### Education Column
- **Graduation** → Graduation (unchanged)
- **PhD** → PhD (unchanged)
- **Master** → Masters
- **Basic** → Basic (unchanged)
- **2n Cycle** → High School

#### Marital Status Column
- **Single** → Single (unchanged)
- **Alone** → Single (merged)
- **Together** → In Relationship
- **Married** → Married (unchanged)
- **Divorced** → Divorced (unchanged)
- **Widow** → Widowed
- **Absurd** → Unknown (invalid entry)
- **YOLO** → Unknown (invalid entry)

### 5. Date Format Conversion
- Converted `customer_date` from string format to datetime
- Original format: dd-mm-yyyy (e.g., "04-09-2012")
- Maintains dd-mm-yyyy format for consistency

### 6. Data Type Corrections

#### Integer Columns
Converted to integer type (int32):
- id, year_birth, kids_home, teens_home
- recency, num_deals_purchases, num_web_purchases
- num_catalog_purchases, num_store_purchases, num_web_visits_month
- accepted_campaign_1 through accepted_campaign_5
- complain, cost_contact, response

#### Float Columns
Converted to float type (int64/float64):
- amount_wines, amount_fruits, amount_meat
- amount_fish, amount_sweets, amount_gold
- revenue

## Files in Repository
marketing-campaign-cleaning/
│
├── task1.ipynb                          # Jupyter notebook with cleaning code
├── marketing_campaign.csv               # Original dataset (tab-separated)
├── marketing_campaign_cleaned.xlsx      # Cleaned dataset
└── README.md                            # This file

## Requirements
```python
pandas>=1.3.0
numpy>=1.21.0
openpyxl>=3.0.0  # For Excel file handling
Install dependencies:
bashpip install pandas numpy openpyxl
Usage
Running the Notebook

Ensure marketing_campaign.csv is in the same directory
Open task1.ipynb in Jupyter Notebook or JupyterLab
Run all cells sequentially
Output file marketing_campaign_cleaned.xlsx will be generated

Using the Cleaned Data
python import pandas as pd
