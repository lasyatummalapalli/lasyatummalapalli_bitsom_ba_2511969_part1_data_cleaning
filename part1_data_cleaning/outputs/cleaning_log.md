# Cleaning Log — Project Summary

This work involved cleaning, validating, and preparing retail order data for business reporting and analysis. The aim was to produce an analysis-ready dataset while keeping the original source file intact and recording every data-quality issue discovered.

## Files

- Source file: `raw_orders.xlsx`
- Cleaned output: `cleaned_orders.xlsx`

## Identified Data Quality Issues

### Text problems

- Inconsistent use of capitalization across many text fields.
- Leading and trailing spaces present.
- Multiple consecutive spaces between words.
- Inconsistent naming for categories and statuses.
- Missing values in some text fields.

### Missing values

- region values missing.
- ship_mode values missing.
- discount values missing.

### Date problems

- Multiple date formats mixed within the same columns.
- Dates stored as text in some cells.
- Invalid date entries found.
- Some ship_date values occur before their corresponding order_date.

### Duplicates

- Exact duplicate records present.
- Duplicate order IDs detected that need investigation.

### Business-rule violations

- Invalid discount values (out of expected range or negative).
- Sales and profit numbers that don’t reconcile with business calculations.
- Transactions marked cancelled, refunded, or failed that need special handling.

## Text cleaning performed

Standardized these fields:

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

### Actions taken:

- Trimmed leading and trailing spaces (TRIM).
- Removed undesirable characters (CLEAN, SUBSTITUTE).
- Standardized capitalization (PROPER).
- Harmonized category and status labels.
- Replaced missing region with "Unknown".
- Replaced missing ship_mode with "Unknown".

## Date cleaning and validation

### Date columns processed:

- order_date
- ship_date

### Date formats found in source:

- 07/27/2024 → MM/DD/YYYY
- 28-11-2024 → DD-MM-YYYY
- 2024-07-21 → YYYY-MM-DD
- 05 Sep 2024 → DD Mon YYYY

Excel serial date values preserved as-is.

### Validation categories applied:

- Valid Date
- Missing Date
- Invalid Date
- Unrecognized Text
- Ship Before Order

### Date-related findings (counts):

- Total records checked: 932
- Missing dates: 0
- Unrecognized date text: 0
- Invalid dates: 1
- Ship date before order date: 22

### Derived date field:

- shipping_delay_days = ship_date − order_date

Negative delays were kept because they flag invalid shipping sequences that need business review.

## Duplicate handling

- Exact duplicate rows were identified and documented.
- Duplicate order IDs were evaluated separately.

### Handling rules:

- Exact duplicates were recorded for reporting.
- Orders with conflicting duplicate IDs were retained but flagged for review.
- No conflicting records were removed without documentation.

## Business rules applied

### Missing values:

- Missing region filled with "Unknown".
- Missing ship_mode filled with "Unknown".

### Discount handling:

- Missing discount replaced with 0 when other sales fields were valid.
- Negative discounts flagged as invalid.
- Discounts outside the acceptable range flagged as invalid.

### Order/payment status rules:

- Cancelled orders excluded from completed-sales reporting.
- Failed payments excluded from completed-sales reporting.
- Refunded transactions summarized separately.

### Shipping rules:

- Ship dates earlier than order dates were flagged as invalid shipping records.

## Calculated columns added

- cleaned_discount
- calculated_sales
- calculated_profit
- profit_margin
- shipping_delay_days
- order_month
- order_year
- data_quality_flag

## Data quality classification

Records were labeled as:

- Clean: no quality issues.
- Warning: minor issues, usable with caution.
- Invalid: major rule violations or validation failures.

## Assumptions

- Discounts are presumed valid between 0 and 1.
- Completed sales require Order Status = Completed and Payment Status = Paid.
- Mixed date formats were interpreted according to the validated patterns identified during assessment.

## Limitations

- Some flagged records require manual business review.
- Duplicate order IDs with conflicting information cannot be auto-resolved.
- Lack of business context prevented authoritative correction of some anomalies.

## Deliverables produced

- cleaned_orders.xlsx
- data_quality_report.xlsx
- pivot_summary.xlsx
- cleaning_log.md
- README.md
- Supporting screenshots