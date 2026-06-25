# Netflix Titles — Data Cleaning & EDA

SQL-based data cleaning and exploratory analysis on the Netflix titles dataset (8,807 records, 2013–2021), with a Power BI dashboard for visualization.

## Overview

| Metric | Value |
|---|---|
| Total Titles | 8,807 |
| Movies | 6,131 (70%) |
| TV Shows | 2,676 (30%) |
| Countries Represented | 748 |
| Date Range | 2013 – 2021 |

## Data Cleaning

| Issue | Count | Action |
|---|---|---|
| Missing director | 2,634 | Filled with "Unknown" |
| Missing country | 831 | Filled with "Unknown" |
| Missing rating | 7 | Filled with "NR" |
| Missing duration | 3 | Filled from `rating` column |
| Duplicate rows | 12 | Removed |
| Invalid ratings | 4 | Corrected to "NR" |
| Date mismatches (`date_added` < `release_year`) | 6 | Flagged for review |

**Standardizations applied:** date format (`YYYY-MM-DD`), text casing (title case / uppercase), whitespace trimming, column naming (`snake_case`), and data types (`date_added` → `DATE`, `duration` → `NVARCHAR`).

## Key Insights

1. **Netflix is movie-first** — Movies make up 70% of content, a ratio consistent across every year in the dataset.
2. **2019 was peak growth** — Content additions dropped ~35% in 2020, coinciding with COVID-19 production halts.
3. **US leads, India is rising** — The US has 3.5x more titles than #2 India, which is Netflix's fastest-growing market.
4. **Adult-skewed audience** — TV-MA and TV-14 ratings account for over 60% of titles; 75%+ targets teens/adults.
5. **International & Drama dominate genres** — These two categories make up ~60% of top-genre content.

## Repo Structure

```
├── scripts/
│   ├── 01_data_cleaning.sql
│   ├── 02_deduplication.sql
│   ├── 03_standardization.sql
│   ├── 04_validation.sql
│   └── 05_eda_queries.sql
├── reports/
│   └── Netflix_Summary_Report.docx
└── README.md
```

## Sample Query

```sql
-- Top 10 content-producing countries
SELECT TOP 10 country, COUNT(*) AS total_titles
FROM netflix_titles
WHERE country IS NOT NULL
GROUP BY country
ORDER BY total_titles DESC;
```

Full scripts: [`scripts/`](./scripts) · Full report: [`reports/Netflix_Summary_Report.docx`](./reports/Netflix_Summary_Report.docx)

## Tools Used
SQL Server · Power BI
