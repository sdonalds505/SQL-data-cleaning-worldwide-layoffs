# SQL-data-cleaning-worldwide-layoffs
SQL data cleaning project for worldwide layoff data

This project demonstrates a complete raw-to-clean data pipeline for a real-world dataset of global layoffs (March 2020–March 2023) using MySQL. While I was familiar with data cleaning in Excel, this repository shows my first experience applying these techniques using SQL. The methodology follows the excellent tutorial by YouTube creator Alex The Analyst

## Dataset
- Source: `layoffs.csv` (~2,300 rows)
- Contains company layoffs with details: company, location, industry, laid-off count, percentage, date, funding stage, country, funds raised, etc.
- Raw data contains duplicates, inconsistent naming, wrong data types, and missing values.

## Objective
Transform the raw `world_layoffs` table into a clean, analysis-ready dataset through systematic data cleaning.

## Data Cleaning Steps Performed

| Step                  | Action Taken                                                                     | Purpose                                 |
|-----------------------|----------------------------------------------------------------------------------|-----------------------------------------|
| 1. Create Staging     | Copied raw data into `layoffs_staging` and `layoffs_staging2`                    | Never modify raw data directly          |
| 2. Remove Duplicates  | Used `ROW_NUMBER() OVER (PARTITION BY ...)` + new table                          | Eliminate exact duplicate records       |
| 3. Standardize Data   | `TRIM()`, fixed "Crypto Currency" → "Crypto", "United States." → "United States" | Ensure consistency                      |
| 4. Fix Data Types     | Converted `date` from text (`mm/dd/yyyy`) → proper `DATE` type                   | Enable time-series analysis             |
| 5. Populate Blanks    | Self-join to fill missing `industry` based on other rows from same company       | Maximize data retention                 |
| 6. Remove Junk Rows   | Deleted rows where both `total_laid_off` and `percentage_laid_off` are NULL      | No meaningful layoff info               |
| 7. Final Cleanup      | Dropped helper column `row_num`                                                  | Clean schema                            |

Final clean table: **`layoffs_staging2`**

## Skills Demonstrated
- CTEs and window functions (`ROW_NUMBER()`)
- Safe duplicate removal in MySQL
- String functions (`TRIM`, `LIKE`, `STR_TO_DATE`)
- Self-joins for data imputation
- Data standardization and quality best practices
