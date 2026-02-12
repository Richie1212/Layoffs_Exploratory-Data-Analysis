-- LAYOFFS DATA EXPLORATION & ANALYSIS (EDA)

-- Purpose: Identify trends, patterns, and outliers in company layoffs

 
-- SECTION 1: INITIAL DATA OVERVIEW

-- Basic sanity check - what does our data look like?
SELECT * 
FROM layoffs_staging2;


-- SECTION 2: SCALE OF LAYOFFS - FINDING EXTREMES

-- What was the largest single layoff event in our dataset?
-- This helps us understand the scale we're dealing with
SELECT MAX(total_laid_off)
FROM layoffs_staging2;


-- What's the range of layoff percentages?
-- This shows us whether companies laid off a few people or entire workforces
SELECT MAX(percentage_laid_off) AS max_percentage,  
       MIN(percentage_laid_off) AS min_percentage
FROM layoffs_staging2
WHERE percentage_laid_off IS NOT NULL;


-- Which companies shut down completely (100% layoff)?
-- These are critical cases - companies that didn't survive the downturn
SELECT *
FROM layoffs_staging2
WHERE percentage_laid_off = 1;


-- Among companies that shut down completely, which ones had raised significant funding?
-- This highlights high-profile failures and burned capital
SELECT *
FROM layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;



-- SECTION 3: BIGGEST IMPACT ANALYSIS - WHO IS LAYING OFF THE MOST?


-- Which companies had the largest single layoff event?
-- Shows which companies made the biggest immediate workforce cuts
SELECT company, 
       total_laid_off
FROM layoffs_staging2
ORDER BY total_laid_off DESC
LIMIT 5;


-- Which companies laid off the most people total (across all layoff events)?
-- Identifies companies with the most severe ongoing restructuring
SELECT company, 
       SUM(total_laid_off) AS total_employees_laid_off
FROM layoffs_staging2
GROUP BY company
ORDER BY total_employees_laid_off DESC
LIMIT 10;



-- SECTION 4: GEOGRAPHIC & INDUSTRY TRENDS


-- Which cities/locations are most affected by layoffs?
-- Helps understand geographic concentration of economic impact
SELECT location, 
       SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY location
ORDER BY total_laid_off DESC
LIMIT 10;


-- Layoffs by country - which markets are being hit hardest?
-- Shows which geographic markets are experiencing the most workforce reductions
SELECT country, 
       SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY country
ORDER BY total_laid_off DESC;


-- Total layoffs by year - is the trend getting better or worse?
-- Critical metric to understand if the crisis is intensifying or improving
SELECT YEAR(date) AS year, 
       SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY YEAR(date)
ORDER BY year ASC;


-- Which industries are most affected?
-- Reveals which sectors of the economy are struggling most
SELECT industry, 
       SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY industry
ORDER BY total_laid_off DESC;


-- Layoffs by company funding stage - does maturity matter?
-- Shows whether startups or mature companies are cutting more
SELECT stage, 
       SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY stage
ORDER BY total_laid_off DESC;



-- SECTION 5: ADVANCED ANALYSIS - YEAR-OVER-YEAR COMPARISON


-- Top 3 companies with biggest layoffs in each year
-- This allows us to see if the same companies are repeatedly cutting,
-- or if different companies are affected in different years
WITH Company_Year AS 
(
  -- First, calculate total layoffs by company and year
  SELECT company, 
         YEAR(date) AS year, 
         SUM(total_laid_off) AS total_laid_off
  FROM layoffs_staging2
  GROUP BY company, YEAR(date)
)
, Company_Year_Rank AS (
  -- Rank companies within each year to find the top 3
  SELECT company, 
         year, 
         total_laid_off, 
         DENSE_RANK() OVER (PARTITION BY year ORDER BY total_laid_off DESC) AS ranking
  FROM Company_Year
)
-- Display only the top 3 for each year
SELECT company, 
       year, 
       total_laid_off, 
       ranking
FROM Company_Year_Rank
WHERE ranking <= 3
  AND year IS NOT NULL
ORDER BY year ASC, total_laid_off DESC;


-- SECTION 6: TREND ANALYSIS - MONTHLY LAYOFF VOLUME


-- Layoffs aggregated by month
-- Shows if there are seasonal patterns or specific periods of crisis
SELECT SUBSTRING(date, 1, 7) AS month, 
       SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY month
ORDER BY month ASC;


-- Cumulative layoffs over time (Rolling Total)
-- Visualizes the ongoing impact and total accumulated layoffs
-- Useful for showing stakeholders the growing/shrinking nature of the crisis
WITH DATE_CTE AS 
(
  -- Group layoffs by month
  SELECT SUBSTRING(date, 1, 7) AS month, 
         SUM(total_laid_off) AS monthly_layoffs
  FROM layoffs_staging2
  GROUP BY month
  ORDER BY month ASC
)
-- Calculate running total to show cumulative impact
SELECT month, 
       SUM(monthly_layoffs) OVER (ORDER BY month ASC) AS cumulative_total_layoffs
FROM DATE_CTE
ORDER BY month ASC;
