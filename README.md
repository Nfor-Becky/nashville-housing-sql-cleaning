# Nashville Housing: Data Cleaning with SQL and Excel

## Business question

Can these property sales records be trusted for analysis? This project focused on identifying data quality issues, correcting errors where possible, and preparing a more reliable dataset for future analysis.

## Dataset

Nashville housing sales from Kaggle  
https://www.kaggle.com/datasets/tmthyjames/nashville-housing-data

56,636 rows and 31 columns. Public data.

## Tools

SQL Server (SSMS) and Excel

## What I did

1. Imported the file with every column as text because the import wizard guessed some data types incorrectly. This allowed me to bring the data in without relying on potentially incorrect automatic conversions, then convert the columns properly during cleaning.
2. Made a working copy and left the raw table untouched.
3. Found that Property_Address and Property_City held each other's data and renamed them back to their correct names.
4. Filled missing addresses using rows with the same Parcel_ID. Missing before: 159, filled: 16, still missing: 143 (flagged in an Address_Missing column).
5. Converted Sale_Date and Sale_Price from text to real date and number types using TRY_CONVERT.
6. Removed 104 duplicate sales (same Parcel_ID, address, price, date and legal reference).
7. Checked Sold_As_Vacant: only Yes and No, so nothing needed to be changed.

## Result

The original dataset contained 56,636 rows. After removing 104 duplicate records, the cleaned dataset contained 56,532 rows.

I also checked the cleaned results in Excel using a pivot table. The totals matched SQL: Yes – 4,889 and No – 51,643.

![Excel check matches SQL](images/05_excel_vs_sql.png)

## Data quality log

| Issue | Rows affected | Fix | Reason |
| --- | ---: | --- | --- |
| Address and city columns swapped | All | Renamed the columns | The column labels did not match the information they contained. Correcting them made the data easier to understand and use. |
| Missing property address | 159 | Filled 16 using the same Parcel_ID and flagged the remaining 143 | Properties with the same Parcel_ID could be used to recover missing addresses. The remaining missing values were flagged rather than guessed. |
| Sale date and price stored as text | All | Used TRY_CONVERT to convert them to date and decimal types | Dates and prices need the correct data types for reliable filtering, calculations and analysis. |
| Duplicate sales | 104 | Removed extra copies | Duplicate records could inflate sales counts and affect calculations and analysis. |
| Sold_As_Vacant check | 0 | No changes needed | The column already contained consistent Yes and No values. |

## Why these columns

I focused on columns that help identify properties and understand their sales, including Parcel_ID, property addresses, Sale_Date and Sale_Price. I also checked Sold_As_Vacant because it provides useful information about the properties. These fields were important for identifying missing information, checking duplicates and preparing the dataset for further analysis.

## What I learned

This project helped me understand how to use SQL to inspect, clean and validate a real-world dataset. I learned how to handle missing values, correct column issues, convert data types and identify duplicates without changing the original data. I also used Excel pivot tables to cross-check my SQL results and improve my confidence in the final dataset.
