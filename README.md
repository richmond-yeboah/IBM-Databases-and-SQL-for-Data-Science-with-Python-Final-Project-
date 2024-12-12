# Database and SQL for Data Science with Python - Final Project

This repository contains my final project submission for the "Database and SQL for Data Science with Python" course. The project involves analyzing datasets from Chicago, including Census data, Crime data, and School data. The goal is to extract meaningful insights by querying and analyzing the data using SQL.

## Project Overview

### Objective
The objective of this project is to:
- Load and analyze data from various sources.
- Use SQL to write and execute queries.
- Derive insights to answer specific questions about the datasets.

### Datasets
The project uses the following datasets:
1. **Census Data**: Contains population demographics for Chicago.
2. **Crime Data**: Includes records of reported crimes in Chicago.
3. **School Data**: Features metrics on school performance.

### Tools Used
- **SQLite**: To manage and query the datasets.
- **Python**: For data loading and integration with SQLite.
- **Jupyter Notebook**: For writing and running SQL queries.
- **Libraries**: `sqlite3`, `pandas`, `matplotlib`, `IPython-SQL`.

---

## Some Key Insights and Queries

### 1. Low-Income Areas
- **Query**: List of community areas with a per capita income below 11,000.
```sql
SELECT COMMUNITY_AREA_NUMBER, COMMUNITY_AREA_NAME, PER_CAPITA_INCOME
FROM CENSUS_DATA
WHERE PER_CAPITA_INCOME < 11000;
```
- **Result**:
  - West Garfield Park: 10,934
  - South Lawndale: 10,402
  - Fuller Park: 10,432
  - Riverdale: 8,201

### 2. Crime-Prone Community Area
- **Query**: Determine the community area with the most crimes.
```sql
SELECT COMMUNITY_AREA_NUMBER
FROM (SELECT COMMUNITY_AREA_NUMBER, COUNT(*)
      FROM CHICAGO_CRIME_DATA
      GROUP BY COMMUNITY_AREA_NUMBER
      ORDER BY COUNT(*) DESC
      LIMIT 1);
```
- **Result**: Community area 25.

### 3. Community Area with Most Crimes
- **Query**: Use a sub-query to find the community area name with the most crimes.
```sql
SELECT COMMUNITY_AREA_NAME
FROM CENSUS_DATA
WHERE COMMUNITY_AREA_NUMBER = (
    SELECT COMMUNITY_AREA_NUMBER
    FROM (SELECT COMMUNITY_AREA_NUMBER, COUNT(*) AS CRIME_COUNT
          FROM CHICAGO_CRIME_DATA
          GROUP BY COMMUNITY_AREA_NUMBER
          ORDER BY CRIME_COUNT DESC
          LIMIT 1));
```
- **Result**: *Austin*.

---

## How to Run
1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```
2. Install required libraries:
   ```bash
   pip install pandas matplotlib ipython-sql
   ```
3. Open the Jupyter Notebook and run the cells step-by-step to execute the queries and analyze the results.

---

## Files in Repository
- **`Final Project.ipynb`**: The Jupyter Notebook containing SQL queries and outputs.
- **`FinalDB.db`**: The SQLite database file containing the datasets.
- **Screenshots**: Results of specific queries.

---

## Key Learnings
This project provided hands-on experience in:
- Writing SQL queries to solve analytical problems.
- Integrating SQL with Python to perform database operations.
- Working with real-world datasets to extract insights.

---
