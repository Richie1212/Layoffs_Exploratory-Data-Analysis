# Layoffs Data Analysis Project

## Overview

This project provides a comprehensive exploratory data analysis (EDA) of company layoffs data, designed to identify trends, patterns, and outliers across industries, geographies, and time periods. The analysis helps business stakeholders understand the scale, scope, and impact of workforce reductions in the tech and broader business sectors.

## Project Purpose

During economic downturns and market corrections, companies across industries implement layoffs as part of restructuring efforts. This project analyzes:

- **Scale of Impact**: How many employees were affected and what percentage of companies were impacted
- **Geographic Trends**: Which regions and countries experienced the most layoffs
- **Industry Patterns**: Which sectors were hit hardest by workforce reductions
- **Temporal Trends**: How layoff activity changed over time
- **Company-Level Analysis**: Which companies made the biggest cuts and which completely shut down

## Data Structure

### Source Table: `layoffs_staging2`

The analysis uses a cleaned and staged version of the layoffs dataset with the following key columns:

| Column | Type | Description |
|--------|------|-------------|
| `company` | VARCHAR | Name of the company |
| `total_laid_off` | INT | Number of employees laid off in the event |
| `percentage_laid_off` | DECIMAL | Percentage of workforce laid off (0-1) |
| `date` | DATE | Date when the layoff was announced |
| `funds_raised_millions` | INT | Total capital the company had raised (in millions) |
| `location` | VARCHAR | City where company headquarters is located |
| `country` | VARCHAR | Country of company headquarters |
| `industry` | VARCHAR | Industry sector the company operates in |
| `stage` | VARCHAR | Company funding stage (Seed, Series A-F, Post-IPO, etc.) |

**Data Coverage**: Layoffs from approximately 2020-2023

## Key Queries & Insights

### Section 1: Scale Analysis
Understand the magnitude of layoffs with maximum values and percentages.

**Key Questions Answered:**
- What was the largest single layoff event?
- What percentage range did companies lay off?
- Which companies shut down completely (100% layoff)?

### Section 2: Impact Rankings
Identify the companies and locations with the most significant layoffs.

**Key Questions Answered:**
- Which companies laid off the most employees total?
- Which cities/locations were most affected?
- What was the geographic distribution?

### Section 3: Industry & Sector Trends
Analyze which industries and company stages were most impacted.

**Key Questions Answered:**
- Which industries experienced the most layoffs?
- Did early-stage startups or mature companies cut more?
- How was impact distributed across funding stages?

### Section 4: Temporal Analysis
Track how layoff activity changed over time.

**Key Questions Answered:**
- Did layoffs increase or decrease year-over-year?
- Which months saw the most activity?
- What's the cumulative impact over time?

### Section 5: Year-Over-Year Comparison
Identify top companies being affected in each year.

**Key Questions Answered:**
- Which companies were hit hardest in each year?
- Are the same companies repeatedly cutting or different ones each year?

## How to Use This Project

### Prerequisites

- SQL database (MySQL, PostgreSQL, SQL Server, etc.)
- Access to the `layoffs_staging2` table
- SQL query client/editor

### Running the Queries

1. **View all comments and query structure:**
   Open `layoffs_eda.sql` in your SQL editor

2. **Run individual sections:**
   Each section is clearly marked with comments. Run queries in order or selectively based on what insights you need.

3. **Copy entire file:**
   Run the entire file to execute all queries in sequence

### Viewing Results

Each query returns specific metrics:
- **Simple queries** return single values or rankings
- **GROUP BY queries** return aggregated summaries
- **CTE queries** return detailed year-over-year and temporal trends

## Key Findings Summary

### Notable Discoveries

1. **Complete Company Shutdowns**: Companies with 100% layoffs (going out of business)
   - Includes both well-known and lesser-known companies
   - Some raised significant venture capital before failure

2. **Concentrated Impact**: Layoffs are not evenly distributed
   - Specific cities and countries show higher concentration
   - Certain industries are more affected than others

3. **Temporal Patterns**: Layoff activity varies by month and year
   - Some periods show sharp increases in activity
   - Rolling totals show cumulative economic impact

4. **Stage Analysis**: Both startups and mature companies are affected
   - Different stages may show different patterns
   - Post-IPO companies may have different dynamics than early-stage

## Data Quality Notes

- The data is staged in `layoffs_staging2` (a cleaned version)
- Some records may have NULL values in specific fields (noted in queries with `WHERE ... IS NOT NULL`)
- Dates are standardized for consistency
- Company names and locations may have minor variations

## SQL Features Used

This analysis demonstrates:

- **Basic Aggregation**: SUM, MAX, MIN functions
- **Grouping**: GROUP BY for multi-dimensional analysis
- **Window Functions**: DENSE_RANK() for ranking within partitions
- **CTEs (Common Table Expressions)**: For complex multi-step queries
- **Date Functions**: YEAR(), SUBSTRING() for temporal analysis
- **Filtering**: WHERE clauses for specific analysis needs

## Files Included

- `README.md` - This file with project overview
- `layoffs_eda.sql` - Complete SQL queries with business-focused comments
- `startup_data.csv` - Supplementary startup funding data (if relevant)

## Recommendations for Stakeholders

When reviewing results from these queries, consider:

1. **Context**: Economic conditions and market trends during the analysis period
2. **Causation**: Layoffs may be driven by company-specific vs. market-wide factors
3. **Timing**: Announcement dates may differ from actual separation dates
4. **Completeness**: Dataset may not capture every layoff event
5. **Future Use**: Use findings for workforce planning and market risk assessment

## Next Steps

Potential extensions to this analysis:

- Predictive modeling on what factors lead to layoffs
- Machine learning classification of "at-risk" companies
- Sentiment analysis of layoff announcements
- Correlation analysis between funding and layoff probability
- Regional economic impact assessment

## Contact & Support

For questions about the queries or data interpretation, refer to the detailed comments within `layoffs_eda.sql` for each section's purpose and business implications.

---
