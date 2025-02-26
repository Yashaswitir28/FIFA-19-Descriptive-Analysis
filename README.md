# FIFA19 Data Analysis

## About
This project involves in-depth data analysis of FIFA19 player statistics using SQL. The analysis includes various queries to derive insights about player attributes, club performances, nationalities, wages, and other key parameters. The dataset is stored in a MySQL database and queried using structured SQL commands.

## Database Setup
### Creating and Using the Database
```sql
CREATE DATABASE fifa19;
USE fifa19;
SELECT * FROM tbl_players;
```

## Analysis Overview
The dataset includes various attributes of FIFA19 players such as nationality, club, wage, overall rating, and more. The analysis focuses on answering key questions related to player distribution, wages, club rankings, and player preferences.

## Key Queries and Insights

### 1. Total Players Count
```sql
SELECT COUNT(*) AS Total_Players FROM tbl_players;
```
- Provides the total number of distinct players.

### 2. Number of Nationalities Represented
```sql
SELECT COUNT(DISTINCT nationality) AS number_of_nationalities FROM tbl_players;
```
- Identifies the unique number of nationalities in the dataset.

### 3. Top Nationalities by Player Count
```sql
SELECT COUNT(*) AS frequency, nationality FROM tbl_players
GROUP BY nationality
ORDER BY frequency DESC
LIMIT 3;
```
- Returns the top 3 nationalities with the highest number of players.

### 4. Wage Analysis (Total, Average, and Standard Deviation)
```sql
ALTER TABLE tbl_players ALTER COLUMN wage FLOAT(50);
SELECT SUM(wage) AS total_wage, AVG(wage) AS average_wage, STD(wage) AS std_wage FROM tbl_players;
```
- Converts wage data type and calculates wage statistics.

### 5. Highest and Lowest Wage Players
```sql
SELECT name FROM tbl_players WHERE wage = (SELECT MAX(wage) FROM tbl_players);
SELECT name FROM tbl_players WHERE wage = (SELECT MIN(wage) FROM tbl_players);
```
- Retrieves the player with the highest and lowest wage.

### 6. Best and Worst Overall Rating Players
```sql
SELECT name FROM tbl_players WHERE overall = (SELECT MAX(overall) FROM tbl_players);
SELECT name FROM tbl_players WHERE overall = (SELECT MIN(overall) FROM tbl_players);
```
- Identifies the highest and lowest-rated players.

### 7. Clubs with Highest Overall Rating
```sql
ALTER TABLE tbl_players ALTER COLUMN overall FLOAT(50);
SELECT SUM(overall) AS total_rating, club FROM tbl_players GROUP BY club ORDER BY total_rating DESC;
```
- Displays clubs with the highest total player rating.

### 8. Top 5 Clubs by Average Player Rating
```sql
SELECT AVG(overall) AS average_rating, club FROM tbl_players GROUP BY club ORDER BY average_rating DESC LIMIT 5;
```
- Returns the top 5 clubs based on player rating.

### 9. Preferred Foot Distribution
```sql
SELECT COUNT(*) AS frequency, preferred_foot FROM tbl_players GROUP BY preferred_foot ORDER BY frequency DESC;
```
- Analyzes left vs. right foot preference among players.

### 10. Luckiest Jersey Number (Highest Wage)
```sql
SELECT jersey_number, SUM(wage) AS total_wage FROM tbl_players GROUP BY jersey_number ORDER BY total_wage DESC LIMIT 1;
```
- Finds the jersey number associated with the highest wage sum.

### 11. Nationality Distribution in Clubs Starting with 'M'
```sql
SELECT COUNT(*) AS freq, nationality, club FROM tbl_players WHERE club LIKE 'M%' GROUP BY nationality, club;
```
- Analyzes player nationality distribution in clubs starting with 'M'.

### 12. Player Transfers within a Date Range
```sql
SELECT COUNT(*) FROM tbl_players WHERE joined BETWEEN '2018-05-20' AND '2019-04-10';
```
- Counts players who joined clubs between May 2018 and April 2019.

### 13. Player Transfers by Date
```sql
SELECT COUNT(*) AS freq, joined FROM tbl_players GROUP BY joined ORDER BY freq DESC;
```
- Analyzes player signings on a daily basis.

### 14. Player Transfers by Year
```sql
SELECT COUNT(*) AS freq, YEAR(joined) FROM tbl_players GROUP BY YEAR(joined) ORDER BY freq DESC;
```
- Analyzes player signings on a yearly basis.

## Summary
This project provides a structured analysis of FIFA19 player data, answering key questions about players, wages, clubs, and transfer statistics. SQL queries are optimized to retrieve valuable insights efficiently. The data can be further visualized in Power BI or other visualization tools for enhanced insights.

---

Thank you for exploring the FIFA19 Data Analysis project! 🚀

