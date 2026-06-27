# Part 1 – Business Data Cleaning, Validation & Excel Reporting

## Project overview

This project involved preparing retail order-level sales data for analysis by cleaning and validating the raw dataset. The original file contained multiple data quality problems, such as inconsistent text formatting, mixed date representations, duplicate entries, missing fields, invalid discounts, and mismatched calculations. The end result is an analysis-ready cleaned dataset, accompanied by data quality documentation and business summary reports.

## Dataset contents

The dataset records retail transactions and includes:

- Order-level details
- Customer attributes
- Product information
- Shipping data
- Sales and profit figures
- Payment status
- Order status

## File handling

The original source file was kept unchanged. All transformations were applied to a separate cleaned dataset.

## Repository layout

```text
part1_data_cleaning/
├── data/
│   ├── raw_orders.xlsx
│   └── cleaned_orders.xlsx
├── outputs/
│   ├── data_quality_report.xlsx
│   ├── pivot_summary.xlsx
│   └── cleaning_log.md
├── screenshots/
│   ├── raw_data_preview.png
│   ├── cleaned_data_preview.png
│   ├── pivot_summary_1.png
│   └── pivot_summary_2.png
└── README.md
```

## Tools and methods

- Microsoft Excel
- Excel formulas
- Pivot tables
- Conditional formatting
- GitHub for version control and repository management

## Data cleaning steps

### Text standardization

Fields normalized include:

- customer_name
- segment
- region
- state
- city
- category
- sub_category
- ship_mode
- payment_status
- order_status

Cleaning actions used:

- Trimming extra whitespace
- Removing unwanted characters
- Unifying capitalization
- Standardizing category and status labels

### Date validation

Validated and corrected:

- order_date
- ship_date

Actions taken:

- Normalized mixed date formats
- Converted textual dates to Excel date values
- Detected invalid dates
- Flagged ship dates occurring before order dates
- Calculated shipping delay in days

### Duplicate handling

- Located exact duplicate rows
- Found duplicate order IDs
- Flagged records with conflicting duplicates
- Recorded the logic used to handle duplicates

### Missing values

Fields and treatments:

- region: filled with "Unknown"
- ship_mode: filled with "Unknown"
- discount: replaced with 0 where appropriate

### Business rules applied

- Set missing region to "Unknown"
- Set missing ship_mode to "Unknown"
- Treat missing discounts as 0 when valid
- Flag negative discounts as invalid
- Flag excessively large discounts as invalid
- Exclude failed payments from completed-sales calculations
- Exclude cancelled orders from completed-sales calculations
- Summarize refunded transactions separately
- Flag records where ship date precedes order date

### Calculated columns added

- cleaned_discount
- calculated_sales
- calculated_profit
- profit_margin
- shipping_delay_days
- order_month
- order_year
- data_quality_flag

## Data quality reporting

The data quality report contains:

- Summary of missing values
- Duplicate record summary
- Invalid discount summary
- Date issues summary
- Order status distribution and issues
- Calculation mismatch summary
- Counts comparing final cleaned records vs. flagged records

## Pivot reports produced

- Sales and profit by region — compare regional revenue and profitability.
- Sales and profit by category and sub-category — analyze product performance.
- Order count by ship mode — distribution of shipping types.
- Profit margin by customer segment — segment-level profitability.
- Refunded, failed, and cancelled orders by region — track operational problems by area.
- Monthly sales trend — time-series sales performance.

## Key business findings

- The South region delivered the highest sales.
- Records labeled Unknown for region reveal data collection gaps that should be investigated.
- Standard Class was the most commonly used shipping method.
- Profitability differs by customer segment and product category.
- Refunded, failed, and cancelled transactions highlight operational and customer experience risks.
- Monthly trends reveal seasonality and performance patterns.

## Assumptions

- Valid discount values range from 0 to 1.
- A sale is considered completed only if order_status is Completed and payment_status is Paid.
- Mixed date strings were interpreted according to the validated formats identified during the analysis.

## Limitations

- Some flagged records require manual review and business judgement.
- Conflicting duplicates with the same order ID could not be resolved automatically.
- No business context was available to confidently correct certain anomalous records.

## Screenshots included

- raw_data_preview.png
- cleaned_data_preview.png
- pivot_summary_1.png
- pivot_summary_2.png

## Deliverables

- Raw dataset
- Cleaned dataset
- Data quality report
- Pivot summary report
- Cleaning log
- Screenshots
- README documentation