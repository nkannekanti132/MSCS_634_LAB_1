# MSCS 634 — Lab 1: Data Analysis with Python

## Purpose

This lab demonstrates a complete **data analytics pipeline** using Python (Pandas, Matplotlib, Seaborn, Scikit-learn) on a retail sales dataset. The workflow covers:

1. **Data Collection** — Loading and exploring a 500-record sales dataset
2. **Data Visualization** — Creating 6 chart types (scatter, line, bar, histogram, box plot, pie)
3. **Data Preprocessing** — Handling missing values, outlier removal (IQR), data reduction, scaling, and discretization
4. **Statistical Analysis** — Central tendency, dispersion measures, and correlation analysis

## Dataset

**File:** `sales_data.csv`  
**Records:** 500 orders | **Columns:** 9

| Column | Description |
|--------|-------------|
| `Order_ID` | Unique order identifier |
| `Date` | Transaction date (2023–2024) |
| `Category` | Product category (Electronics, Clothing, Sports, Books, Home & Kitchen) |
| `Region` | Geographic region (North, South, East, West) |
| `Units_Sold` | Number of units sold |
| `Unit_Price` | Price per unit ($) |
| `Discount_Pct` | Discount percentage applied |
| `Customer_Rating` | Customer satisfaction rating (1–5) |
| `Revenue` | Total revenue generated ($) |

## Key Insights

### Visualizations
- **Units Sold vs Revenue**: Strong positive correlation — higher unit sales generally drive higher revenue, though discount rates introduce variability.
- **Monthly Revenue Trend**: Revenue fluctuates month to month without a clear seasonal pattern; occasional spikes are driven by large individual orders.
- **Category Revenue**: Categories differ in average revenue; Electronics and Sports tend to generate higher per-order revenue.
- **Customer Ratings**: Ratings are roughly uniformly distributed (1–5), showing no strong satisfaction bias.
- **Regional Revenue**: Median revenue is fairly similar across all four regions; outliers exist in every region.
- **Sales Volume**: Unit sales are distributed relatively evenly among the five categories.

### Statistical Analysis
- **Correlation**: `Units_Sold` and `Revenue` show a moderate positive correlation (~0.5). `Discount_Pct` has a weak negative relationship with `Revenue`.
- **Dispersion**: Revenue has the highest variance, reflecting its wide range across orders. `Customer_Rating` has the lowest variance.
- **Outliers**: ~10 extreme revenue values were detected via the IQR method and removed for cleaner analysis.

## Preprocessing Decisions
- **Missing Values**: `Customer_Rating` filled with **median**, `Region` filled with **mode** (most frequent region), `Discount_Pct` filled with **median**.
- **Outlier Removal**: Used the **IQR method** (1.5×IQR rule) on `Revenue` to remove extreme values.
- **Data Reduction**: Dropped `Order_ID` (non-analytical identifier); demonstrated 60% random sampling.
- **Scaling**: Applied both **Min-Max normalization** and **Z-Score standardization** to numeric columns for comparison.
- **Discretization**: Converted `Customer_Rating` into categorical bins (Low / Medium / High).

## Challenges & Decisions
- **Synthetic data characteristics**: Since the dataset is synthetically generated, some real-world patterns (e.g., seasonality) are absent, but this was useful for demonstrating the full preprocessing pipeline.
- **Missing value strategy**: Chose median/mode imputation over deletion to preserve the dataset size for analysis. Median was preferred over mean for `Customer_Rating` and `Discount_Pct` to reduce the influence of potential skew.
- **Outlier threshold**: The 1.5×IQR rule was selected as a standard, widely-accepted method. A few very large revenue values (likely data anomalies) were successfully identified and removed.
- **Scaling trade-offs**: Both Min-Max and Z-Score were demonstrated to show their different behaviors — Min-Max bounds values to [0, 1], while Z-Score centers around 0 with unit variance.

## Screenshots

All visualizations and analysis outputs are saved in the `/screenshots` folder:

| # | Screenshot | Description |
|---|-----------|-------------|
| 1 | `01_data_overview.png` | Dataset shape, columns, and data types |
| 2 | `02_scatter_units_vs_revenue.png` | Scatter plot — Units Sold vs Revenue |
| 3 | `03_line_monthly_revenue.png` | Line chart — Monthly average revenue trend |
| 4 | `04_bar_avg_revenue_by_category.png` | Bar chart — Average revenue by category |
| 5 | `05_histogram_customer_ratings.png` | Histogram — Customer rating distribution |
| 6 | `06_boxplot_revenue_by_region.png` | Box plot — Revenue distribution by region |
| 7 | `07_pie_sales_by_category.png` | Pie chart — Sales volume by category |
| 8 | `08_missing_values.png` | Missing values detection & handling |
| 9 | `09_outlier_detection.png` | Outlier detection before/after (IQR) |
| 10 | `10_data_scaling.png` | Min-Max vs Z-Score scaling comparison |
| 11 | `11_central_tendency.png` | Central tendency measures table |
| 12 | `12_dispersion_measures.png` | Dispersion measures table |
| 13 | `13_correlation_heatmap.png` | Correlation matrix heatmap |

## Repository Structure

```
Assignmentt/
├── MSCS_634_Lab_1.ipynb    # Jupyter Notebook with full analysis
├── sales_data.csv          # Dataset (500 records)
├── README.md               # This file
└── screenshots/            # All visualization screenshots
    ├── 01_data_overview.png
    ├── 02_scatter_units_vs_revenue.png
    ├── 03_line_monthly_revenue.png
    ├── 04_bar_avg_revenue_by_category.png
    ├── 05_histogram_customer_ratings.png
    ├── 06_boxplot_revenue_by_region.png
    ├── 07_pie_sales_by_category.png
    ├── 08_missing_values.png
    ├── 09_outlier_detection.png
    ├── 10_data_scaling.png
    ├── 11_central_tendency.png
    ├── 12_dispersion_measures.png
    └── 13_correlation_heatmap.png
```

## Tools & Libraries

- **Python 3**
- **Pandas** — Data manipulation
- **NumPy** — Numerical operations
- **Matplotlib** — Plotting
- **Seaborn** — Statistical visualizations
- **Scikit-learn** — MinMaxScaler, StandardScaler
