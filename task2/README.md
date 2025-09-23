# Superstore Data Analytics Project - Task 2

## Project Overview

This project contains a comprehensive analysis of the Sample Superstore dataset, including data exploration, visualization, business insights, and dashboard creation using Python and Power BI.

## 📁 Files in this Directory

### 📊 Data Files
- **`Sample - Superstore.csv`** (2.3MB) - Original dataset with 9,994 rows and 21 columns
- **`superstore_data.xlsx`** (1.3MB) - Cleaned Excel version of the original data
- **`superstore_power_bi_data.xlsx`** (1.7MB) - Multi-sheet Excel file prepared for Power BI with summary tables

### 📈 Analysis & Visualizations
- **`superstore_analysis.ipynb`** (719KB) - Complete Jupyter notebook with data analysis and Python visualizations
- **`task2_visuals.pbix`** (695KB) - Power BI dashboard file with interactive visualizations
- **`powerBI_graphs.pdf`** (714KB) - PDF export of Power BI visualizations

## 🔍 Analysis Process

### 1. Data Exploration & Preprocessing
- **Data Loading**: Imported CSV data and converted to Excel format
- **Data Cleaning**: Verified data quality (no missing values found)
- **Feature Engineering**: Created derived columns including:
  - Time-based features (Year, Month, Quarter, Weekday)
  - Business metrics (Profit Margin, Days to Ship)
  - Discount tiers for analysis
- **Data Types**: Converted date columns to proper datetime format

### 2. Business Metrics Analysis

#### Key Performance Indicators
- **Total Sales**: $2,297,201
- **Total Profit**: $286,397
- **Profit Margin**: 12.47%
- **Annual Growth**: 14.8% CAGR (2014-2017)
- **Average Order Value**: $229.86
- **Customer Base**: 793 unique customers
- **Product Portfolio**: 1,850 unique products

#### Performance by Category
1. **Technology**: 17.4% profit margin (Best performing)
2. **Office Supplies**: 17.0% profit margin
3. **Furniture**: 2.5% profit margin (Needs attention)

#### Regional Performance
1. **West**: Highest sales and profitability
2. **East**: Strong performance
3. **South**: Moderate performance
4. **Central**: Lowest profit margins (7.92%)

### 3. Problem Areas Identified

#### High-Impact Issues
- **Furniture Category**: Extremely low 2.5% margin
- **Tables Sub-category**: $17,725 in losses
- **High Discounts**: 1,166 orders with >30% discount causing losses
- **Loss-making Products**: 301 products (16.3%) operating at a loss

#### Discount Impact Analysis
- **Correlation**: -0.219 between discount and profit
- **High discounts (>30%)**: Consistently unprofitable
- **Optimal range**: 0-10% discount tier shows highest profitability

### 4. Growth Opportunities

#### Immediate Actions (0-3 months)
1. Cap discounts at 25% maximum
2. Review furniture pricing and supplier contracts
3. Discontinue worst-performing products

#### Short-term Strategy (3-12 months)
1. Expand Technology products to underperforming regions
2. Focus on Home Office segment (highest margins)
3. Optimize Q4 seasonal planning

#### Potential Impact
- **Discount reform**: Could improve margins by 2-3 percentage points
- **Regional optimization**: Potential $125,000+ additional sales
- **Product portfolio cleanup**: Eliminate $18,053 in losses

## 🛠️ Technical Implementation

### Python Libraries Used
```python
pandas          # Data manipulation and analysis
numpy           # Numerical computations
matplotlib      # Data visualization
seaborn         # Statistical visualizations
datetime        # Date/time handling
openpyxl        # Excel file operations
```

### Analysis Workflow
1. **Data Import & Quality Check**
2. **Exploratory Data Analysis (EDA)**
3. **Time Series Analysis**
4. **Profitability Analysis**
5. **Customer & Product Segmentation**
6. **Discount Impact Assessment**
7. **Business Insights Generation**
8. **Data Export for Power BI**

### Power BI Dashboard Features
- **Executive Summary**: Key metrics and KPIs
- **Sales Performance**: Trends and seasonality
- **Regional Analysis**: Geographic performance mapping
- **Product Portfolio**: Category and sub-category breakdown
- **Profit Optimization**: Discount and margin analysis
- **Customer Insights**: Segmentation and behavior patterns

## 📊 Key Visualizations Created

### Python Matplotlib/Seaborn Charts
1. **Sales Performance Analysis** (2x2 grid):
   - Annual sales & profit trends
   - Monthly seasonality patterns
   - Category performance comparison
   - Regional sales distribution

2. **Top Performers Analysis** (2x2 grid):
   - Top 10 sub-categories by profit
   - Top 10 states by sales
   - Customer segment performance
   - Regional profit comparison

3. **Problem Areas Analysis** (2x2 grid):
   - Loss-making sub-categories
   - Profit margins by category
   - Top 10 loss-making products
   - Regional profit margins

4. **Discount Impact Analysis** (2x2 grid):
   - Discount vs profit scatter plot
   - Average profit by discount tier
   - Discount rate distribution
   - Profit margins by discount level

### Power BI Interactive Dashboards
- Dynamic filtering and drill-down capabilities
- Geographic mapping for regional analysis
- Time-based slicers for temporal analysis
- Cross-filtering between related visualizations

## 📈 Business Recommendations

### Priority 1 (Critical)
- **Discount Policy**: Implement maximum 25% discount cap
- **Furniture Review**: Investigate supplier contracts and pricing
- **Product Pruning**: Discontinue consistently loss-making items

### Priority 2 (High Impact)
- **Regional Expansion**: Replicate Technology success in Central/South
- **Segment Focus**: Increase Home Office market penetration
- **Seasonal Strategy**: Optimize Q4 inventory and marketing

### Priority 3 (Strategic)
- **Customer Analysis**: Develop retention programs for top customers
- **Supply Chain**: Optimize shipping times and costs
- **Market Expansion**: Explore new product categories with high margins

## 🚀 Getting Started

### Prerequisites
```
Python 3.7+
Jupyter Notebook
Power BI Desktop
```

### Required Python Packages
```bash
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

### Running the Analysis
1. Open `superstore_analysis.ipynb` in Jupyter Notebook
2. Run all cells to reproduce the analysis
3. Open `task2_visuals.pbix` in Power BI Desktop for interactive dashboards

## 📁 Data Dictionary

### Main Dataset Columns
- **Row ID**: Unique identifier for each row
- **Order ID**: Unique identifier for each order
- **Order Date / Ship Date**: Transaction timestamps
- **Customer Info**: ID, Name, Segment
- **Geography**: Country, City, State, Region, Postal Code
- **Product Info**: ID, Category, Sub-Category, Name
- **Metrics**: Sales, Quantity, Discount, Profit

### Derived Columns
- **Year/Month/Quarter**: Time-based groupings
- **Days_to_Ship**: Shipping duration
- **Profit_Margin**: Profit as percentage of sales
- **Discount_Tier**: Categorized discount ranges

## 📋 Summary Statistics

| Metric | Value |
|--------|--------|
| **Data Period** | 2014-01-03 to 2017-12-30 |
| **Total Transactions** | 9,994 |
| **Unique Orders** | 5,009 |
| **Unique Customers** | 793 |
| **Unique Products** | 1,850 |
| **Geographic Coverage** | 49 states, 531 cities |
| **Average Shipping Time** | 4.0 days |

---

*Analysis completed on September 23, 2025*
*For questions or additional analysis, refer to the Jupyter notebook for detailed methodology*